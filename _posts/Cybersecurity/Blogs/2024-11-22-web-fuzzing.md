---
layout: post
title: Web Fuzzing
date: 2024-11-22 20:52 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://media.licdn.com/dms/image/sync/v2/D4D27AQEywhT4MhgD6A/articleshare-shrink_800/articleshare-shrink_800/0/1725882207137?e=2147483647&v=beta&t=D6OeFikPcXy27yu0NlLMsMbwqZPjvH5Wt68UA1AdRhA
---

## Hvad er fuzzing?
Fuzzing er en testteknik, hvor man sender forskellige typer brugerinput til en grænseflade for at analysere, hvordan systemet reagerer. For eksempel:

- Ved fuzzing efter SQL-injektionssårbarheder sender vi tilfældige specialtegn og observerer serverens svar.
- Ved fuzzing for buffer overflow sender vi lange strenge af tekst og øger længden gradvist for at se, om programmet bryder sammen.

Når vi udfører fuzzing på webapplikationer, bruger vi ofte foruddefinerede ordlister med almindeligt anvendte termer. Dette skyldes, at webservere sjældent giver en oversigt over tilgængelige links og mapper (medmindre de er dårligt konfigurerede). Vi tester forskellige links for at se, hvilke der returnerer sider.

**Eksempel:**  
- Besøger vi en ikke-eksisterende side som:  
  `https://www.example.com/doesnotexist`,  
  får vi HTTP-koden 404 Page Not Found.  

- Besøger vi en eksisterende side som:  
  `https://www.example.com/login`,  
  får vi login-siden og HTTP-koden 200 OK.  

Dette er grundideen bag fuzzing: Vi tester en masse mulige sider og analyserer serverens svar for at finde ud af, hvilke der findes.

## Automatisering af fuzzing
At teste manuelt ville tage uendelig lang tid. Derfor bruger vi værktøjer som ffuf, der kan sende hundredevis af forespørgsler hvert sekund. Disse værktøjer analyserer HTTP-svarkoderne og afgør hurtigt, hvilke sider der eksisterer. Herefter kan vi manuelt undersøge de fundne sider.

## Wordlists
For at finde eksisterende sider og mapper på et website anvender vi ordlister. Disse lister indeholder ofte brugte ord og navne for webmapper og sider.

Selvom fuzzing ikke altid afslører alle sider (fx sider med tilfældige eller unikke navne), kan vi ofte finde op til 90% af siderne på et website ved at bruge gode ordlister.

## Hvor finder man wordlists?
Vi behøver ikke lave disse lister selv. Mange eksisterende ordlister er allerede skabt ved at undersøge nettet for almindelige webdirektorier og filnavne. Et af de mest populære steder at finde sådanne ordlister er GitHub SecLists, som har en omfattende samling kategoriseret efter forskellige typer fuzzing.

Disse inkluderer også lister over almindeligt brugte adgangskoder, som fx. kan bruges til Password Brute Forcing.

## Sammenfatning
Fuzzing er en effektiv metode til at finde skjulte sider og mapper på websites. Ved at bruge værktøjer som ffuf og gode ordlister kan vi hurtigt identificere sider og derefter analysere deres indhold manuelt. Det er et afgørende værktøj inden for sikkerhedstestning og en vigtig del af at afdække potentielle sårbarheder.
