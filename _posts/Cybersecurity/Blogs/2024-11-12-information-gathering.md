---
layout: post
title: Information Gathering
date: 2024-11-12 12:20 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: assets/informationgathering.png
---

Når vi forsøger at udnytte sårbarheder i en penetrationstest, er det baseret på den information, vi indsamler om vores mål. Denne fase er selve fundamentet for enhver penetrationstest. Informationen kan hentes på mange forskellige måder, men vi kan opdele processen i følgende kategorier:
- Open-Source Intelligence (OSINT)
- Infrastruktur-Enumeration
- Service-Enumeration
- Host-Enumeration

Disse fire trin er nødvendige i hver penetrationstest, da den indsamlede information er afgørende for at identificere sårbarheder og gennemføre en succesfuld test. Informationen kan findes mange steder, fx på sociale medier, jobopslag, individuelle værter og servere eller via medarbejdere. Information er overalt, fordi mennesker (og netværk) konstant udveksler data.

## Open-Source Intelligence (OSINT)
OSINT indebærer at finde offentligt tilgængelig information om en virksomhed eller personer, som kan afsløre værdifulde detaljer som møder, interne og eksterne relationer eller afhængigheder. Denne information kan komme fra offentlige kilder som hjemmesider, sociale medier eller repositories.

**Eksempel:**
- **Kode og nøgler:** Mange udviklere deler utilsigtet følsomme oplysninger, som adgangskoder eller SSH-nøgler, på platforme som GitHub. Hvis disse oplysninger findes, skal de rapporteres og håndteres i overensstemmelse med aftalte regler (RoE - Rules of Engagement).
- **Uønskede delinger:** Udviklere kan også dele kode på fora som StackOverflow, hvilket utilsigtet kan afsløre virksomhedens interne detaljer.  

OSINT gør det muligt for penetrationstestere at finde og rapportere sådanne sårbarheder, så de kan lukkes.

## Infrastruktur-Enumeration
Denne fase fokuserer på at skabe et overblik over virksomhedens netværk både på internettet (eksternt) og internt (intranet). Her anvendes OSINT og aktive scanninger for at kortlægge servere og værter samt netværkets struktur.

**Mål og teknikker:**  
- Identifikation af netværkskomponenter: Fx navneservere (DNS), mailservere, cloudinstanser osv.
- Analyse af sikkerhedsforanstaltninger: Fx firewalls og sikkerhedspolitikker, der kan hjælpe os med at udføre angreb uden at blive opdaget.  

**Eksempel:**  
Hvis vi identificerer en netværkskomponent, kan vi forsøge at udføre et angreb som Password Spraying, hvor én adgangskode testes på mange brugernavne for at opnå adgang.

## Service-Enumeration  
Her fokuserer vi på de tjenester, der kører på netværket eller på individuelle værter og servere. Målet er at finde ud af:

- Hvilke tjenester kører, og hvilken version der bruges.
- Om tjenesten har kendte sikkerhedshuller.  

**Udfordringer og observationer:**  
- Ældre versioner: Mange administratorer undgår at opdatere systemer, da det kan påvirke funktionaliteten. Dette efterlader ofte sikkerhedshuller, som kan udnyttes.
- Analyse af formål: Ved at forstå, hvorfor en tjeneste eksisterer, kan vi forudsige, hvordan den kan udnyttes.

## Host-Enumeration
Efter at have kortlagt infrastrukturen, undersøger vi hver vært (host) for at finde:

- Hvilket operativsystem og hvilke tjenester der kører.
- Versionshistorik og potentielle sårbarheder.

**Eksempel:**
- **Misconfigurerede systemer:** En FTP-server med anonym adgang kan være en sårbarhed.
- **Ældre enheder:** Mange værter bruger software, der ikke længere understøttes af producenten, men som stadig kan findes på netværket.  

**Intern vs. Ekstern analyse:**
- **Eksternt:** Vi ser på, hvad der kan tilgås fra internettet.
- **Internt:** Vi udforsker interne tjenester og ressourcer, der ofte er mindre sikrede, fordi de ikke er offentligt tilgængelige.

## Post-Exploitation og internt host-analyse
Når vi har udnyttet en sårbarhed, undersøger vi værten yderligere indefra:

- Vi leder efter følsomme filer, scripts, adgangskoder og andre ressourcer.
- Disse data kan bruges til at forhøje rettigheder eller udføre yderligere angreb.  

## Sammenfatning
Processen med enumeration er en afgørende del af penetrationstestning. Den opdeler arbejdet i fire trin, hvor hver kategori hjælper med at identificere sikkerhedshuller og kortlægge målets infrastruktur. Fra offentligt tilgængelig information (OSINT) til interne analyser af værter, er målet at finde svagheder, som kan udnyttes, og rapportere dem, så de kan afhjælpes. Dette gør virksomhedens sikkerhed stærkere på sigt.
