---
layout: post
title: Implementering af videoReducer og videoContext
date: 2024-11-22 21:31 +0000
categories: [React, React/blog]
image: https://miro.medium.com/v2/resize:fit:1400/1*OLdS7KqIA_4f1RHu0-YtsQ.jpeg
---

## Implementering af useReducer og Context

- Initialisering af reducer og state:

``` javascript
const [videos, dispatch] = useReducer(VideoReducer, []);
```

  - useReducer bruges til at administrere tilstanden (videos) og til at opdatere denne tilstand med dispatch.
  - Reduceren, VideoReducer, håndterer logikken for, hvordan tilstanden ændres baseret på de handlinger, der sendes til dispatch.

- Handlinger i reduceren (dispatch):

  - fetchVideos:
    - Henter en liste over videoer fra serveren og opdaterer tilstanden med dispatch({ type: "getAllVideos", payload: data.videos }).
  - saveVideo:
    - Tilføjer en ny video til tilstanden ved at sende addVideo-handlingen med den nye video som payload.
  - updateVideo:
    - Opdaterer en eksisterende video ved hjælp af updateVideo-handlingen og den opdaterede video som payload.
  - deleteVideo:
      - Fjerner en video fra tilstanden ved at sende deleteVideo-handlingen og videoens id som payload.

- Kontekst og provider (VideoContext.Provider):

  - Reducerens tilstand og opdateringsfunktioner (videos, saveVideo, updateVideo, deleteVideo, fetchVideos) deles med resten af applikationen via VideoContext.Provider.

## VideoContext og useVideo hook

- VideoContext er en React-kontekst, der giver adgang til videos og reducerens funktioner.
- useVideo er et custom React-hook, der gør det nemt for komponenter at tilgå konteksten:

``` javascript
export const useVideo = () => {
    return useContext(VideoContext);
};
```

Dette gør det muligt at bruge videos og de tilhørende funktioner uden at skulle skrive useContext(VideoContext) manuelt.

## Hvordan det bruges i projektet
- I VideoPage:

  - useVideo bruges til at tilgå videos og metoder som fetchVideos fra konteksten.
  - fetchVideos henter videoer og initialiserer reducerens tilstand.
  - Når brugeren udfører en handling som at tilføje, opdatere eller slette en video, kaldes saveVideo, updateVideo, eller deleteVideo. Disse sender handlinger til reduceren via dispatch.

- I VideoForm:

  - Når en video oprettes eller opdateres, kalder formularen enten saveVideo eller updateVideo, som opdaterer tilstanden via reduceren.

## Fordele ved brug af reducer og context
- Centraliseret tilstandshåndtering:

Reduceren håndterer logikken ét sted, hvilket gør koden lettere at vedligeholde og debugge.

- Kontekst for deling af tilstand:

VideoContext gør det nemt at dele tilstanden (videos) og reducerens funktioner på tværs af komponenter uden at skulle "prop-drille".

- Forenklet komponentlogik:

Komponenter som VideoPage og VideoForm behøver kun at kalde relevante funktioner fra useVideo-hooket, hvilket gør dem mere fokuserede og lettere at teste.
