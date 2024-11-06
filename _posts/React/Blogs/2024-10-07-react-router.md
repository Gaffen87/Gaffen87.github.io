---
layout: post
title: react-router
date: 2024-10-07 12:39 +0000
categories: [React, React/blog]
image: assets/reactrouterlogo.avif
---

## React Router

React Router er et populært bibliotek til håndtering af navigation og routing i en React-applikation. Det gør det muligt at bygge single page applications (SPA), hvor man kan navigere mellem forskellige "sider" eller visninger uden at genindlæse hele siden. React Router giver dig mulighed for at kontrollere, hvad der vises på skærmen, baseret på URL'en, samtidig med at applikationen forbliver hurtig og dynamisk.

Efter studering af den officielle [dokumentation](https://reactrouter.com) tilhørende React Router er her et sammenskriv af de vigtigste funktionaliteter:

#### **BrowserRouter:**
En komponent, der omslutter hele din applikation og håndterer historikken for browserens URL. Det er den primære container for alle routing-komponenter.

``` jsx
import { BrowserRouter } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      {/* Andre komponenter og routes */}
    </BrowserRouter>
  );
}
```
#### **Routes og Route:** 
Disse bruges til at definere, hvilke komponenter der skal vises baseret på den aktuelle URL. Routes omslutter de enkelte Route-komponenter, som hver repræsenterer en rute.

``` jsx
import { Routes, Route } from 'react-router-dom';

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
    </Routes>
  );
}
```
#### **Link:** 
En komponent, der fungerer som et anker-element `<a>`, men uden at genindlæse hele siden, når man navigerer. Det giver mulighed for at navigere rundt i applikationen.

``` jsx
import { Link } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
}
```
#### **useNavigate:** 
En hook, der bruges til programmatisk navigation, så du kan flytte brugeren til en ny rute uden at bruge et Link.

``` jsx
import { useNavigate } from 'react-router-dom';

function GoBackButton() {
  const navigate = useNavigate();

  return (
    <button onClick={() => navigate(-1)}>Tilbage</button>
  );
}
```

#### **Dynamiske Ruter**
I mange tilfælde vil du have brug for dynamiske ruter, hvor en del af URL'en ændrer sig afhængigt af data. Dette kan gøres med parameterbaserede ruter.

Eksempel på en dynamisk rute, der matcher forskellige ID'er:

``` jsx
import { Routes, Route } from 'react-router-dom';

function App() {
  return (
    <Routes>
      <Route path="/product/:productId" element={<ProductPage />} />
    </Routes>
  );
}
```

Her vil URL'er som /product/1, /product/2, osv. blive håndteret af samme ProductPage-komponent. For at hente productId i komponenten bruges useParams-hooken:

```jsx
import { useParams } from 'react-router-dom';

function ProductPage() {
  const { productId } = useParams();

  return <h1>Produkt ID: {productId}</h1>;
}
```

#### **Nested Routes**
React Router tillader også indlejrede ruter, som gør det muligt at have flere niveauer af navigation. Dette er især nyttigt, hvis du har en layout-komponent, der omslutter flere undersider.

``` jsx
import { Routes, Route, Outlet } from 'react-router-dom';

function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>
      <Outlet /> {/* Hvor undersiderne rendres */}
    </div>
  );
}

function App() {
  return (
    <Routes>
      <Route path="dashboard" element={<Dashboard />}>
        <Route path="profile" element={<Profile />} />
        <Route path="settings" element={<Settings />} />
      </Route>
    </Routes>
  );
}
```
I dette eksempel bliver Dashboard-komponenten rendret, og derefter vises enten Profile eller Settings komponenter afhængig af URL'en (/dashboard/profile eller /dashboard/settings). Outlet-komponenten angiver, hvor undersiderne skal rendres.

#### **useLocation**
useLocation-hooken giver adgang til den nuværende URL (placering). Den kan bruges til at få mere kontrol over navigationen eller til at reagere på URL-ændringer i realtid.

```jsx
import { useLocation } from 'react-router-dom';

function LocationDisplay() {
  const location = useLocation();

  return <div>Nu befinder du dig på: {location.pathname}</div>;
}
```

#### **useNavigate og Historikkontrol**
Med useNavigate kan du navigere programmæssigt til en bestemt rute eller tilbage i historikken. Du kan også angive state, der bliver sendt sammen med navigationen.

``` jsx
import { useNavigate } from 'react-router-dom';

function HomeButton() {
  const navigate = useNavigate();

  return (
    <button onClick={() => navigate('/', { state: { from: 'dashboard' } })}>
      Gå til Home
    </button>
  );
}
```
Den state, du sender her, kan tilgås via useLocation i målruten. Dette er meget nyttigt, når man skal sende kontekstuel information under navigation.

#### **Redirects**
Nogle gange vil du måske omdirigere brugeren til en anden rute, f.eks. hvis de forsøger at få adgang til en beskyttet side uden at være logget ind. Dette kan gøres med Navigate-komponenten:

```jsx
import { Navigate } from 'react-router-dom';

function ProtectedPage({ isLoggedIn }) {
  if (!isLoggedIn) {
    return <Navigate to="/login" replace />;
  }

  return <h1>Beskyttet Side</h1>;
}
```
Her vil Navigate omdirigere brugeren til login-siden, hvis de ikke er logget ind.

