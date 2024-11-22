---
layout: post
title: Bug Bounties
date: 2024-11-22 21:09 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://miro.medium.com/v2/resize:fit:1024/0*ZwZGevBfDuq8qlg-.png
---

Et bug bounty-program kan bedst beskrives som en crowdsourcing-indsats, hvor enkeltpersoner bliver anerkendt og kompenseret for at finde og rapportere fejl i software. Men Bug bounty-programmer kan også beskrives som en proaktiv og kontinuerlig sikkerhedstest, der supplerer interne kodegennemgange og penetrationstests og spiller en vigtig rolle i en organisations sårbarhedsstyring.

For eksempel beskriver HackerOne deres bug bounty-platform som: "Konstant testning, konstant beskyttelse", og deres løsning kan nemt integreres i organisationens eksisterende udviklingscyklus.

## Typer af bug bounty-programmer
Bug bounty-programmer kan være enten private eller offentlige:

**Private bug bounty-programmer**
- Ikke offentligt tilgængelige.
- Kun udvalgte bug bounty-jægere kan deltage, og det kræver ofte en specifik invitation.
- Programmer starter ofte som private for at give organisationen tid til at lære at håndtere rapportering og triagering af sårbarheder.
- Invitationer tildeles baseret på en jægers tidligere resultater, evnen til at finde gyldige sårbarheder og fravær af regelovertrædelser.
- Nogle private programmer kan kræve en baggrundstjek.

**Offentlige bug bounty-programmer**
- Åbne for hele hackingfællesskabet.
- Alle kan deltage og indsende rapporter.

**Parent/Child-programmer**
- En virksomhed (parent) og dens datterselskaber (child) deler samme belønningspulje og sikkerhedsteam. Et child-program er knyttet til parent-programmet.

## Forskellen mellem Bug Bounty Program (BBP) og Vulnerability Disclosure Program (VDP)
- VDP: En sårbarhedsafsløringsproces, hvor en organisation beskriver, hvordan den ønsker at modtage oplysninger om sårbarheder.
- BBP: Motiverer eksterne til at finde og rapportere sårbarheder med økonomisk belønning.
- VDP er vejledende, mens BBP er belønningsbaseret.

## Adfærdskodeks for bug bounty-jægere
En bug bounty-jægers tidligere overtrædelser vægtes altid højt. Derfor er det vigtigt at overholde programmets adfærdskodeks. Dette forbedrer ikke kun jægerens effektivitet, men øger også chancen for succes. For eksempel indeholder HackerOne’s Code of Conduct retningslinjer, der hjælper med at balancere professionalitet og teknisk kunnen.

## Struktur i et bug bounty-program
Bug bounty-programmer består typisk af følgende elementer:

- **Vendor Response SLAs:** Hvornår og hvordan virksomheden vil besvare rapporter.
- **Adgang:** Hvordan man opretter eller får adgang til konti til forskning.
- **Berettigelseskriterier:** Fx at være den første til at rapportere en sårbarhed.
- **Ansvarlig afsløringspolitik:** Regler for sikker offentliggørelse af sårbarheder.
- **Regler for deltagelse:** Retningslinjer for testmetoder.
- **Scope:** Definerer, hvad der kan testes (fx IP-adresser, domæner, applikationer).
- **Out of Scope:** Hvad der ikke må testes.
- **Rapporteringsformat:** Hvordan rapporter skal udformes.
- **Belønninger:** Økonomiske eller andre former for kompensation.
- **Safe Harbor:** Beskyttelse mod juridisk ansvar for god tro.
- **Juridiske vilkår:** Kontraktmæssige forhold.
- **Kontaktinformation:** Hvor og hvordan man kan indsende rapporter.

## Politik og struktur
Politikken for et bug bounty-program beskriver, hvordan en organisation ønsker at modtage rapporter om potentielle sårbarheder. Den angiver programmets omfang og skaber klare rammer for jægere. For at forstå strukturen kan man studere programmer som Alibaba BBP og Amazon Vulnerability Research Program på HackerOne-platformen.

## Sammenfatning 
Bug bounty-programmer er en essentiel del af moderne cybersikkerhed og giver virksomheder mulighed for at afdække og håndtere sårbarheder hurtigt og effektivt. For bug bounty-jægere er det vigtigt at balancere teknisk dygtighed og professionalisme for at opnå succes.

# At skrive en god rapport
For at rapportere sikkerhedsproblemer effektivt er det vigtigt at præsentere fund på en klar og præcis måde, så sikkerheds- eller triageteamet hurtigt kan forstå problemet. En god rapport bør indeholde alle nødvendige detaljer, inklusive en trin-for-trin-vejledning til at genskabe problemet.

## Nøglen til en god rapport
Når man rapporterer til mindre erfarne organisationer, kan det være nødvendigt at forklare tekniske sikkerhedsproblemer i forretningsmæssige termer, så de forstår konsekvenserne. En god rapport indeholder typisk følgende elementer:

- Sårbarhedens titel

Beskriv kort typen af sårbarhed, det påvirkede domæne/parameter/endpoint, og dens potentielle konsekvens.

- CWE og CVSS-score

Brug CWE (Common Weakness Enumeration) til at klassificere sårbarhedstypen og CVSS (Common Vulnerability Scoring System) til at kommunikere problemets alvor.

- Beskrivelse af sårbarheden

Forklar årsagen til sårbarheden og de tekniske detaljer bag den.

- Proof of Concept (PoC)

Giv en klar og præcis trin-for-trin-guide til at demonstrere og genskabe udnyttelsen af sårbarheden.

- Konsekvensanalyse

Uddybd, hvad en angriber kan opnå ved fuldt ud at udnytte sårbarheden, herunder forretningsmæssige konsekvenser og maksimal skade.

- Forslag til udbedring

Selvom dette er valgfrit i bug bounty-programmer, kan det være nyttigt at foreslå, hvordan problemet kan løses.

- Formatering og klarhed

En velstruktureret og letlæselig rapport minimerer tiden, der bruges på at genskabe og validere problemet, og fremskynder triage-processen.

## CWE og CVSS
**CWE (Common Weakness Enumeration)**  
CWE er en liste udviklet af fællesskabet, der beskriver typer af software- og hardware-svagheder. Den fungerer som et fælles sprog og værktøj til at identificere og forhindre svagheder. I tilfælde af kædede sårbarheder skal man vælge en CWE, der beskriver den oprindelige svaghed.

**CVSS (Common Vulnerability Scoring System)**  
CVSS bruges globalt til at beskrive alvoren af en sårbarhed.

## Brug af CVSS Calculator
CVSS v3.1 kan bruges til at vurdere sårbarhedens alvor. Nedenfor gennemgås de vigtigste parametre i **Base Score**-området.

- **Angrebsvektor**

  - **Netværk (N):** Angreb muligt via netværket (fjerntilgængelig).
  - **Adjacent (A):** Angreb kræver samme netværk (f.eks. VPN).
  - **Lokal (L):** Angreb kræver fysisk eller fjernadgang (SSH, terminal).
  - **Fysisk (P):** Angreb kræver fysisk manipulation.

- **Angrebskompleksitet**

  - **Lav (L):** Ingen særlige forberedelser kræves for at udføre angrebet.
  - **Høj (H):** Særlige forberedelser eller dataindsamling er nødvendige.

- **Nødvendige privilegier**

  - **Ingen (N):** Ingen særlige rettigheder kræves.
  - **Lav (L):** Standardbrugeradgang kræves.
  - **Høj (H):** Administratorniveau kræves.

- **Brugerinteraktion**

  - **Ingen (N):** Angrebet kan udføres uden brugerens handling.
  - **Kræves (R):** Brugeren skal interagere for at muliggøre angrebet.

- **Scope (Omfang)**

  - **Uændret (U):** Kun den sårbare komponent påvirkes.
  - **Ændret (C):** Andre komponenter påvirkes også.

- **Konfidentialitet**

  - **Ingen (N):** Ingen kompromittering af fortrolighed.
  - **Lav (L):** Noget information afsløres, men angriberen har begrænset kontrol.
  - **Høj (H):** Betydelig eller total afsløring af fortrolige oplysninger.

- **Integritet**

  - **Ingen (N):** Ingen ændringer i data.
  - **Lav (L):** Begrænsede ændringer i data med minimal konsekvens.
  - **Høj (H):** Alvorlige eller totale ændringer i data.

- **Tilgængelighed**

  - **Ingen (N):** Ingen effekt på systemets tilgængelighed.
  - **Lav (L):** Nedsat ydeevne eller adgang.
  - **Høj (H):** Total eller alvorlig forringelse af tilgængelighed.

Ved at bruge CVSS kan man objektivt og standardiseret kommunikere en sårbarheds alvor til organisationer og hjælpe dem med at prioritere rettelser.
