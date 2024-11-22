---
layout: post
title: Lateral Movement
date: 2024-11-22 15:38 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://academy.hackthebox.com/storage/modules/90/0-PT-Process-LA.png
---

Når vi har haft succes med at trænge ind i virksomhedens netværk (Exploitation), indsamlet lokalt lagrede data og eskaleret vores privilegier (Post-Exploitation), bevæger vi os videre til Lateral Movement-fasen. Her tester vi, hvad en angriber kunne gøre i hele netværket. Målet er ikke kun at udnytte et enkelt system, men også at finde følsomme data og identificere måder, hvorpå en angriber kunne forstyrre eller lamme netværket. Et velkendt eksempel er ransomware, der kan kryptere systemer på tværs af hele netværket og gøre dem utilgængelige, indtil en dekrypteringsnøgle leveres.

Denne fase belyser konsekvenserne af dårlig IT-sikkerhed. Mange virksomheder opdager først betydningen af robust sikkerhed, når de står over for økonomiske tab eller juridiske konsekvenser, fx på grund af manglende beskyttelse af kundedata. I mange lande kan virksomhedens øverste ledelse gøres ansvarlig for sådanne sikkerhedsbrud.

## Mål og trin i Lateral Movement-fasen
Målet i denne fase er at udforske netværket og teste, hvor langt en angriber kunne nå. Vi undersøger, hvilke interne sårbarheder der kan udnyttes og følger disse trin:

- Pivoting (adgang til skjulte netværksområder)
- Evasive Testing (undgå opdagelse)
- Information Gathering (indsamling af information)
- Vulnerability Assessment (vurdering af sårbarheder)
- (Privilege) Exploitation (udnyttelse af rettigheder)
- Post-Exploitation (håndtering af de nye systemer)

I nogle tilfælde kan vi ikke eskalere privilegier direkte på ét system, men vi kan bevæge os til andre dele af netværket via Lateral Movement.

## Pivoting (Omdirigering af angreb)
Pivoting gør det muligt at bruge det kompromitterede system som en proxy, så vi kan angribe andre systemer i det interne netværk. Dette er især vigtigt, når vi forsøger at nå netværksområder, der normalt ikke er tilgængelige udefra (fx interne subnetværk). Den kompromitterede vært videresender vores forespørgsler til interne systemer.

**Eksempel:**  
Forestil dig, at en printer på et hjemmenetværk ikke kan nås fra internettet. Men hvis en computer på dette netværk kompromitteres, kan vi bruge den som en mellemstation for at sende kommandoer til printeren. Dette enkle eksempel viser princippet bag pivoting – at opnå adgang til ellers utilgængelige systemer.

## Evasive Testing (Undgåelse af opdagelse)
Som i tidligere faser skal vi vurdere, om evasive testing er nødvendig. Når vi forsøger at bevæge os gennem netværket, kan overvågningsværktøjer som IPS/IDS, mikrosegmentering og EDR registrere vores handlinger. For at undgå opdagelse analyserer vi først, hvordan disse sikkerhedssystemer fungerer, og tilpasser vores metoder derefter.

## Information Gathering (Indsamling af information)
Inden vi retter angreb mod netværket, skal vi kortlægge det. Vi undersøger:

- Hvor mange systemer der kan nås.
- Hvilke tjenester, applikationer og enheder der er tilgængelige.

Denne informationsindsamling foregår fra et internt perspektiv, hvilket giver os en ny synsvinkel på netværket sammenlignet med tidligere faser.

## Vulnerability Assessment (Vurdering af sårbarheder)
Inde i netværket undersøger vi sårbarheder på baggrund af interne forhold. Ofte er der flere fejl internt i netværket, da systemer og brugere deler oplysninger og ressourcer.

**Eksempel:** Hvis vi kompromitterer en bruger fra en udviklergruppe, kan vi få adgang til udviklingsværktøjer og ressourcer, som potentielt afslører kritiske oplysninger om virksomhedens systemer.

## (Privilege) Exploitation (Udnyttelse af rettigheder)
Når vi har fundet mulige angrebsveje, prioriterer vi dem og bruger dem til at få adgang til andre systemer. Almindelige metoder inkluderer:

- Knækning af adgangskoder eller hashes.
- Pass-the-Hash-teknikker, hvor vi anvender en opsnappet hash til at logge ind på andre systemer uden at dekryptere den.

For eksempel kan vi bruge værktøjet Responder til at opsnappe NTLMv2-hashes og derefter logge ind som administrator.

## Post-Exploitation (Efterudnyttelse af nye systemer)
Når vi har adgang til flere systemer, gentager vi trin fra post-udnyttelsesfasen:

- Indsamling af systemdata og følsomme oplysninger.
- Analyse af, hvordan de nye oplysninger kan bruges strategisk i netværket.

Vi skal altid tage hensyn til kontraktens retningslinjer for håndtering af følsomme data og sikre, at vi rapporterer resultaterne korrekt til kunden.
