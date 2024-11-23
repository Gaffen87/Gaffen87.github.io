---
layout: post
title: React Context
date: 2024-11-22 13:24 +0000
categories: [React, React/blog]
image: assets/context.png
---

I React er Context en mekanisme, der gør det muligt at dele data mellem komponenter i en applikation uden at skulle videresende props manuelt gennem hvert niveau af komponenttræet. Det er især nyttigt, når du har data eller tilstand, der skal være tilgængelig for mange komponenter på forskellige niveauer i træet.

## Hvordan fungerer Context i React?
1. **Oprettelse af Context:** Du bruger React.createContext() til at oprette en Context.  
Denne metode genererer to ting:

- En Provider komponent, som bruges til at levere data.
- En Consumer, der bruges af komponenter til at få adgang til data.
``` jsx
const MyContext = React.createContext();
```

2. **Provider:**

- Context’s Provider komponent bruges til at pakke de komponenter, der skal have adgang til dataene.
- Du leverer data til alle child components via value-proppen.  

``` jsx
<MyContext.Provider value={someData}>
    <ChildComponent />
</MyContext.Provider>
```

1. **Consumer:**

- En Consumer bruges til at få adgang til data fra Context.
- Det kan gøres enten med MyContext.Consumer eller React’s useContext hook (anbefalet i moderne React).

``` jsx
<MyContext.Consumer>
    {value => <div>{value}</div>}
</MyContext.Consumer>
```  

Eller ved brug af useContext:  

``` jsx
import { useContext } from 'react';

const value = useContext(MyContext);
```  

## Eksempel på brug af Context
1. Opret Context:  

{% raw %}
``` jsx
import React, { createContext, useState } from 'react';

const ThemeContext = createContext();

const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

    return (
        <ThemeContext.Provider value={{ theme, setTheme }}>
            {children}
        </ThemeContext.Provider>
    );
};

export { ThemeContext, ThemeProvider };
```  
      {% endraw %}

1. Brug Context i en komponent:

``` jsx
import React, { useContext } from 'react';
import { ThemeContext } from './ThemeContext';

const ThemeToggler = () => {
    const { theme, setTheme } = useContext(ThemeContext);

    return (
        <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
            Skift tema til {theme === 'light' ? 'dark' : 'light'}
        </button>
    );
};

export default ThemeToggler;
```  

1. Indpak applikationen med Provider:

``` jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { ThemeProvider } from './ThemeContext';
import ThemeToggler from './ThemeToggler';

const App = () => (
    <ThemeProvider>
        <ThemeToggler />
    </ThemeProvider>
);

ReactDOM.render(<App />, document.getElementById('root'));
```  

## Hvornår bruges Context?
Context bør bruges, når:

- Data skal være tilgængelige for mange komponenter uden at bruge "prop-drilling".
- Eksempler på typiske brugsscenarier:
  - Temaer (f.eks. lys/mørk tilstand).
  - Sprogindstillinger.
  - Autentificeringsoplysninger (f.eks. brugerstatus eller token).

## Begrænsninger ved Context
1. Ydelsesproblemer:

- Hvis Context ændrer sig ofte, kan det medføre unødvendige genrenderinger af alle forbrugende komponenter.
- Overvej at memoize værdier med React.memo eller bruge Redux/Zustand for mere komplekse tilstande.

2. Overforbrug:

- Brug ikke Context til alt. Hvis dataene kun skal deles mellem få nært beslægtede komponenter, kan props være tilstrækkeligt.

Context er en kraftfuld måde at håndtere delte data i React, men bør bruges med omtanke for at undgå unødig kompleksitet eller ydeevneproblemer.
