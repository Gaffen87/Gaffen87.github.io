---
layout: post
title: useReducer
date: 2024-10-29 10:51 +0000
categories: [React, React/blog]
image: assets/useReducer.png
---

# React Hook: useReducer

useReducer er et React-hook, som giver en måde at håndtere mere kompleks state-logik end det, som useState tillader. Den er nyttig, når din state har mange forskellige værdier eller når ændringer i state kræver avanceret logik. useReducer fungerer lidt ligesom state-håndtering i Redux, men er mindre kompleks og indbygget direkte i React.

## Hvordan useReducer fungerer
useReducer tager to primære argumenter:

**Reducer-funktionen:** En funktion, som bestemmer, hvordan state skal opdateres baseret på en given action.  
**Initial state:** Startværdien for din state.  

``` javascript
const [state, dispatch] = useReducer(reducer, initialState);
```  

**state** er den nuværende state.  
**dispatch** er en funktion, som bruges til at sende en action til reduceren for at ændre state.  

## Reducer-funktion
Reducer-funktionen modtager to parametre:

- Den aktuelle state.
- En action, som beskriver, hvilken ændring vi vil foretage i state. Reducer-funktionen returnerer en ny state baseret på action-typen.

``` javascript
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}
```

## Simpelt eksempel
Her er et simpelt eksempel, der bruger useReducer til en tæller:

```javascript
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </div>
  );
}
```

**I dette eksempel:**

- `dispatch({ type: 'increment' })` sender en action til reduceren, som øger tælleren.
- `dispatch({ type: 'decrement' })` sender en action, som sænker tælleren.  

**Hvornår skal man bruge useReducer?**
Man kan overveje at bruge useReducer når:

- State har mange forskellige værdier, eller når flere komponenter skal håndtere det samme state.
- Ændringer i state kræver komplekse logikker, der ikke håndteres let med useState.
