---
layout: post
title: Burp Suite
date: 2024-11-12 13:21 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: assets/burplogo.png
---

Burp Suite er et kraftfuldt værktøjssæt til sikkerhedstest af webapplikationer. Det bruges bredt bl.a. af pen testere til at identificere og udnytte sikkerhedssårbarheder i webapplikationer. Burp Suite fungerer som en proxyserver, der opsnapper og analyserer HTTP/S-trafik mellem en klient (browser) og en server.

# Vigtiste funktioner i Burp Suite

## Intercepting Proxy:

![](../assets/proxy.png)

Burp Suite's hovedfunktion er Proxyen. Proxyen gør det muligt for Burp at fungere som en mellemmand mellem klienten (webbrowseren) og serveren, der hoster webapplikationen.

Ved at placere sig mellem disse to komponenter, kan Burp opsnappe alle udvekslinger og anmodninger, der foretages mellem webbrowseren og serveren. Penetrationstesteren vil derfor være i stand til at analysere anmodningerne i detaljer og, hvis det ønskes, ændre dem.

For at ændre anmodninger opsnapper Proxyen anmodninger én ad gangen og lader penetrationstesteren vælge, om de skal sendes videre eller afvises. Hvis de sendes videre, kan de ændres, før de overføres til serveren.

Proxyen giver også mulighed for at se historikken af anmodninger live, uden at de manuelt skal sendes til serveren. Faktisk er dette Proxyens mest brugte tilstand.

## Repeater:

![](../assets/repeater.png)

Repeater er modulet, der gør det muligt at afspille anmodninger efter behov. Som navnet antyder, kan penetrationstesteren gentage anmodninger og ændre dem, som det ønskes, før de sendes til serveren.

Derefter kan testeren analysere serverens svar baseret på de ændringer, der er blevet foretaget. Repeater bruges ofte til manuelt at identificere og udnytte sårbarheder.

## Intruder:

![](../assets/intruder.png)

Intruder er et kraftfuldt værktøj, der kan bruges til at automatisere afsendelsen af en anmodning, der indeholder en tilpasset payload. For eksempel kan Intruder bruges til automatisk at øge en værdi og sende hver inkrement til serveren. Intruder gør det muligt for penetrationstesteren at automatisere kedelige opgaver, som ville være umulige at udføre manuelt, såsom at sende flere tusinde anmodninger. Mulighederne for at bruge Intruder er næsten uendelige, og det giver mulighed for at tilføje flere payloads af samme eller forskellige typer.

Intruder har en "Positions"-fane, hvor penetrationstesteren kan definere positionen af payloaden i anmodningen. Derefter kan han vælge, hvilken type payload der skal injiceres i "Payloads"-fanen.

Typiske anvendelsesområder
- Sårbarhedstest: Identificere sikkerhedshuller som XSS, CSRF, SQL Injection, osv.
- Sikkerhedsanalyser: Teste og validere sikkerhedsimplementeringer i webapplikationer.
- Udvikling og debugging: Analysere og rette fejl i webapplikationer.
- Træning og læring: Brugt i uddannelsesmiljøer til at lære om webapplikationssikkerhed.
