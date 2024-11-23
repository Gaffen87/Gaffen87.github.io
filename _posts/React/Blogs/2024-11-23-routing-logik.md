---
layout: post
title: Routing logik
date: 2024-11-23 21:02 +0000
categories: [React, React/blog]
image: https://blog.openreplay.com/images/understanding-react-router-with-a-simple-blog-application/images/hero.png
---

## Overordnet koncept
React Router matcher URL'en med bestemte ruter og viser komponenter baseret på matchene. Det giver os en `<Route />` component til at definere ruter og en `<Link />` component til navigation. Her laver vi vores egne versioner af Route og Link komponenterne.

## Eksempel-applikation
Lad os se på, hvordan vi vil bruge vores egen router i en simpel applikation:

``` jsx
const Home = () => <h2>Home</h2>;
const About = () => <h2>About</h2>;
const Topic = ({ topicId }) => <h3>{topicId}</h3>;

const Topics = () => {
  const topics = [
    { name: "Rendering with React", slug: "rendering" },
    { name: "Components", slug: "components" },
    { name: "Props v. State", slug: "props-v-state" },
  ];

  const currentPath = window.location.pathname;

  return (
    <div>
      <h2>Topics</h2>
      <ul>
        {topics.map(({ name, slug }) => (
          <li key={slug}>
            <Link to={`/topics/${slug}`}>{name}</Link>
          </li>
        ))}
      </ul>
      {topics.map(({ slug, name }) =>
        currentPath.endsWith(slug) ? <Topic key={slug} topicId={name} /> : null
      )}
    </div>
  );
};

export default function App() {
  return (
    <div>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/topics">Topics</Link>
          </li>
        </ul>
      </nav>
      <hr />
      <Route path="/" exact>
        <Home />
      </Route>
      <Route path="/about">
        <About />
      </Route>
      <Route path="/topics">
        <Topics />
      </Route>
    </div>
  );
}
```

## Implementering af Route
En Route-komponent matcher URL'en og viser dens children, hvis der er et match.

``` jsx
import { useEffect, useState } from "react";

const Route = ({ path, exact, children }) => {
  const [currentPath, setCurrentPath] = useState(window.location.pathname);

  useEffect(() => {
    const handlePopState = () => setCurrentPath(window.location.pathname);
    window.addEventListener("popstate", handlePopState);
    return () => window.removeEventListener("popstate", handlePopState);
  }, []);

  const pathMatch = exact
    ? currentPath === path
    : currentPath.startsWith(path);

  return pathMatch ? children : null;
};
``` 

## Implementering af Link
En Link-komponent giver en deklarativ måde at navigere på uden at genindlæse siden.

``` jsx
const Link = ({ to, children }) => {
  const handleClick = (event) => {
    event.preventDefault();
    window.history.pushState({}, "", to);
    const popStateEvent = new PopStateEvent("popstate");
    window.dispatchEvent(popStateEvent);
  };

  return (
    <a href={to} onClick={handleClick}>
      {children}
    </a>
  );
};
``` 

## Sådan fungerer det

**1. Route:**

- Tjekker, om den nuværende URL matcher path.
- Hvis der er et match, viser den children.

**2. Link:**

- Opdaterer browserens URL via history.pushState uden at genindlæse siden.
- Udløser en popstate-event, så alle Route-komponenter genberegner deres match.

**3. State Management:**

- Vi bruger React's useState til at holde styr på URL'en i hver Route.
- useEffect lytter på ændringer i URL'en.

## Komplet kode

``` jsx
import React, { useState, useEffect } from "react";

const Route = ({ path, exact, children }) => {
  const [currentPath, setCurrentPath] = useState(window.location.pathname);

  useEffect(() => {
    const handlePopState = () => setCurrentPath(window.location.pathname);
    window.addEventListener("popstate", handlePopState);
    return () => window.removeEventListener("popstate", handlePopState);
  }, []);

  const pathMatch = exact
    ? currentPath === path
    : currentPath.startsWith(path);

  return pathMatch ? children : null;
};

const Link = ({ to, children }) => {
  const handleClick = (event) => {
    event.preventDefault();
    window.history.pushState({}, "", to);
    const popStateEvent = new PopStateEvent("popstate");
    window.dispatchEvent(popStateEvent);
  };

  return (
    <a href={to} onClick={handleClick}>
      {children}
    </a>
  );
};

const Home = () => <h2>Home</h2>;
const About = () => <h2>About</h2>;
const Topic = ({ topicId }) => <h3>{topicId}</h3>;

const Topics = () => {
  const topics = [
    { name: "Rendering with React", slug: "rendering" },
    { name: "Components", slug: "components" },
    { name: "Props v. State", slug: "props-v-state" },
  ];

  const currentPath = window.location.pathname;

  return (
    <div>
      <h2>Topics</h2>
      <ul>
        {topics.map(({ name, slug }) => (
          <li key={slug}>
            <Link to={`/topics/${slug}`}>{name}</Link>
          </li>
        ))}
      </ul>
      {topics.map(({ slug, name }) =>
        currentPath.endsWith(slug) ? <Topic key={slug} topicId={name} /> : null
      )}
    </div>
  );
};

export default function App() {
  return (
    <div>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/topics">Topics</Link>
          </li>
        </ul>
      </nav>
      <hr />
      <Route path="/" exact>
        <Home />
      </Route>
      <Route path="/about">
        <About />
      </Route>
      <Route path="/topics">
        <Topics />
      </Route>
    </div>
  );
}
```

Denne løsning viser, hvordan man kan bygge en simpel router uden afhængigheder, samtidig med at man bruger moderne React-teknikker som hooks. Dette giver et godt grundlag for at forstå, hvordan routing fungerer bag kulisserne.
