---
layout: post
title: React Frameworks
date: 2024-11-12 13:19 +0000
categories: [React, React/blog]
image: assets/frameworks.png
---

# ![Vite](../assets/vite.png)
## Vite

Vite er et værktøj til at udvikle frontend-applikationer og er designet med fokus på hastighed og en god udvikleroplevelse.  
Det kan bruges med forskellige frameworks som Vue, Svelte, Solid og selvfølgelig React.

Vite hjælper med at scaffolde en ny applikation og kommer med nogle default templates som gør det nemt at komme igang.

Man starter en ny applikation med kommandoen:
'npm create vite@latest <navn-på-app>'
Herefter vælger man framework og om man vil bruge javascript eller typescript.  
Vite giver dig en hurtig dev server som automatisk opdaterer ændringer i koden til ens browser ved at køre kommandoen:
'npm run dev'  

Vite hjælper dermed med en masse opsætning ift udvikling i React som man så ikke behøver at tænke på. Dog går Vite ikke ind og ændrer noget ved selve måden man udvikler på i React. Man skal stadig selv sørge for at få implementeret fx routing og lign.

Da Vite ikke går ind og roder ved måden man udvikler i React er det hvad jeg har valgt at gå med som framework til dette projekt

---

# ![NextJS](../assets/nextjs.png)
## NextJS

Next.js er et framework udviklet af Vercel som bygger på React. Det har unikke funktioner sammenlignet med andre frameworks, såsom server-side rendering og forbedret SEO (søgemaskineoptimering). Det tilbyder en indbygget routing-funktion, som er folder-baseret.

Funktioner i NextJS
- Hot Code Reloading: Så snart der gemmes ændringer i din kode, afspejles de automatisk i brugergrænsefladen.
- Server Rendering: Next.js' rendering-funktion gør det muligt at gengive React-komponenter på serveren først, inden de sendes til HTML-klienten, hvilket hjælper med at forbedre SEO.
- Automatisk Routing: I ethvert projekt bliver filer i pages-mappen automatisk kortlagt og kræver ikke ekstra kodning for routing.
- Prefetching: Link-komponenten, der bruges til at forbinde forskellige sider, understøtter forudindlæsning af ressourcer i baggrunden.

NextJS er et kæmpe framework som det kræver en del tid at sætte sig ind i, da det også kan fungere som en full-stack løsning med server og frontend.
Da jeg gerne vil fokusere på React i sig selv, synes jeg at NextJS bygger for mange ekstra ting på som vil kræve ekstra tid at sætte sig ind i.

---

# ![Remix](../assets/remix.png)
## Remix

Remix er ligesom NextJS et full-stack framework, som faktisk bygger ovenpå Vite og React.

Funktioner i Remix:
- Dataindlæsning: Remix bruger loaders til at hente data på serveren, før siden gengives.
- Nem routing: Det tilbyder et filbaseret routing-system, hvor routing sker automatisk baseret på de mapper og filer, du opretter. Denne funktion understøttes også i Next.js.
- Server-side rendering (SSR): Remix understøtter SSR for at levere bedre ydeevne og hurtigere sideindlæsning.
- Formularer og handlinger: Remix inkluderer indbygget support til formularhåndtering og actions, hvilket gør det nemt og effektivt at håndtere formularindsendelser og tilhørende handlinger.

Ligesom NextJS indeholder Remix rigtig mange løsninger på ting som ikke er indbygget i React.

Både NextJS og Remix er helt klart frameworks som det ville være smart at lære at kende, men det kommer til at ligge lidt udenfor scope for dette semester.
