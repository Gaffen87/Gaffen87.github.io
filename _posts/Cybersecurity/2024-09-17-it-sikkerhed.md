---
layout: post
title: IT-Sikkerhed
date: 2024-09-17 11:21 +0000
pin: true
description: Her er et overblik over emnet IT-sikkerhed
image: assets/CybersecurityIcon.webp
---

## Opsummering af semester

Min læring inden for IT-sikkerhed, med fokus på penetrationstests (pentests), har været en spændende og intensiv rejse, hvor jeg har opnået en dybere forståelse af sikkerhedsrisici og metoder til at identificere og afhjælpe dem. Min tilgang har været praksisorienteret og baseret på en kombination af teoretisk opbygning og hands-on erfaring med værktøjer og teknikker.

Jeg begyndte med at opbygge en grundlæggende forståelse af pentesting ved at læse artikler og se YouTube-videoer om emner som OWASP Top 10, sikkerhedsmetodologier og typiske angrebsvektorer. Dette gav mig indsigt i, hvordan sårbarheder opstår, og hvordan de kan udnyttes.

Herefter gik jeg i dybden med praktiske øvelser på platforme som TryHackMe og HackTheBox, hvor jeg trænede i at anvende værktøjer og udføre forskellige typer angreb. Disse platforme gav en struktureret måde at udforske emner som rekognoscering, scanning, udnyttelse og rapportering.

**Jeg har fokuseret på værktøjer som:**

- **OWASP ZAP:** Til at analysere og teste sikkerheden i webapplikationer.
- **Nmap:** Til netværksscanning og identifikation af åbne porte og tjenester.
- **Metasploit:** Til automatisering af angreb og simulering af exploits.
- **Wireshark:** Til overvågning og analyse af netværkstrafik.
- **SQLmap:** Til at identificere og udnytte SQL-injektionssårbarheder.

Derudover har jeg brugt **OWASP Juice Shop**, en sårbar webapplikation, som et træningsmiljø til at teste og øve det, jeg har lært. Dette har givet mig mulighed for at simulere realistiske angreb i et sikkert miljø.

Min læringsproces kulminerede i anvendelsen af pentesting på mit semesterprojekt, hvor jeg har forsøgt at identificere sårbarheder og sikre applikationen mod potentielle angreb. Dette inkluderede test af API'er, validering af input og vurdering af sikkerhedsforanstaltninger mod OWASP Top 10.

Gennem denne proces har jeg opnået en stærkere forståelse af sikkerhedskoncepter og en praktisk erfaring med værktøjer og teknikker, der gør mig bedre rustet til at identificere og afhjælpe sikkerhedstrusler i fremtidige projekter.

## Blog posts for emnet

<ul>
  {% for post in site.categories["IT-sikkerhed/blog"] %}
    {% if post.url %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>
