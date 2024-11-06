---
layout: post
title: Task Manager exercise med useReducer
date: 2024-10-29 10:54 +0000
categories: [React, React/blog]
image: assets/taskmanager.png
---

# Introduktion til useReducer opgave

[Introduktion til useReducer](../usereducer)  
Til at lære og øve brugen af useReducer hook'et i React, har jeg valgt at benytte chatgpt til at stille mig en øvelse som passer.
ChatGPT gav mig følgende øvelse:

## Exercise: Building a Simple Task Manager with useReducer
### Goal:
Build a simple task manager application using React and the useReducer hook to handle state. The app will allow users to add tasks, mark them as completed, and delete them.

### App Requirements:
**1. Task Management:**  
- Users should be able to add a task with a description.  
- Tasks should be displayed in a list, showing whether they are completed or not.  
- Users should be able to mark tasks as completed or not completed.  
- Users should be able to delete tasks.    

**2. Filtering Tasks:**  
Users should be able to filter tasks by:
All tasks.
Completed tasks.
Incomplete tasks.  

**3. State Management:**  
The app state (tasks, their completion status, filters) should be managed via the useReducer hook.

## Reducer funktionen
Efter en hurtig opsætning af layout og en grov udgave af appens indhold gik jeg igang med reducer funktionen som indeholder de forskellige actions som en task kan gå igennem:

``` jsx
export const taskReducer = (state, action) => {
	switch (action.type) {
		case "setTasks": {
			return { ...state, tasks: action.payload };
		}
		case "addTask": {
			return {
				...state,
				tasks: [...state.tasks, action.payload],
			};
		}
		case "updateTask": {
			console.log(action.payload);
			return {
				...state,
				tasks: state.tasks.map((task) =>
					task.id === action.payload.id ? action.payload : task
				),
			};
		}
		case "deleteTask": {
			return {
				...state,
				tasks: state.tasks.filter((task) => task.id !== action.payload),
			};
		}
		case "setFilter": {
			return { ...state, filter: action.payload };
		}
	}
};
```
Funktionens parametre indeholde en state og et action objekt. Action indeholder en type som er en string der fortæller funktionen hvad den skal gøre. Derudover indeholder action objektet også en payload (det kan kaldes hvad man har lyst, men jeg har valgt payload overalt for at være konsistent). Payload kan fx bestå af en task, som det ses i "addTask" action-typen.

## Implementering af reducer i app
``` jsx
const initialState = {
	tasks: [],
	filter: "all",
};

function App() {
	const [state, dispatch] = useReducer(taskReducer, initialState);
```
Reducer funktionen implementeres ved at initialisere den med useReducer hooket. Her returneres state og dispatch. Selve hooket skal bruge en reducer funktion og en initial state som parametre. Her har jeg givet den min reducer funktion fra før og en initial state som er et objekt indeholdene et tasks array og en filter attribut.

## dispatch
dispatch er en funktion som bruges til at kalde reduceren. Funktionen skal bruge et action objekt som parameter. Action objektet består typisk af et type attribut plus evt. flere attributer. I eksemplet består mit action objekt af typen "setFilter" og et payload som er type af filter ("all", "completed", "incomplete")
``` jsx
const handleFilter = (filter) => {
		dispatch({ type: "setFilter", payload: filter });
	};
```

## Refleksion
Jeg synes at fremgangsmåden med at bruge chatGPT til at stille en udfordring virkede rigtig godt. Dette tvinger mig til at følge nogle krav, som jeg ikke selv er 100% herre over. Implementeringen af useReducer hooket foregik forholdsvist nemt, dog ramte jeg en udfordring ift. at få implementeret filtreringsfunktionen, hvor det jo var et krav at det skulle være igennem en reducer.

Det fungerer rigtig godt at bruge den officiele dokumentation fra React så meget som muligt og derefter søge hjælp andetsteds, hvis jeg sidder fast et sted. Det giver en god veksling mellem at lære brugen af dokumentation og søgning af information op nettet.

## Næste skridt
Jeg vil bruge den samme applikation til at lære om og implementere Context i React, da Context og Reducer kan kombineres til at håndtere global state for en app.
