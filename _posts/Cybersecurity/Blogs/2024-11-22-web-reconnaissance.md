---
layout: post
title: Web Reconnaissance
date: 2024-11-22 20:00 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://miro.medium.com/v2/resize:fit:892/1*8ImUyzQYz0lWoC5F7ae3QQ.png
---

**Web Reconnaissance** er grundlaget for en grundig sikkerhedsvurdering. Det handler om systematisk at indsamle oplysninger om et målrettet website eller en webapplikation. Dette er forberedelsesfasen, der går forud for mere dybdegående analyser og mulige angreb. Det er en vigtig del af "Information Gathering"-fasen i penetrationstestprocessen.

## Hovedmål for Web Reconnaissance
- **Identifikation af aktiver:**

  Kortlægning af alle offentligt tilgængelige dele af målet, fx websider, underdomæner, IP-adresser og anvendte teknologier. Dette giver et komplet overblik over målets online tilstedeværelse.

- **Find skjulte oplysninger:**

  Opdage følsomme data, der utilsigtet er gjort tilgængelige, som fx backupfiler, konfigurationsfiler eller intern dokumentation. Disse oplysninger kan afsløre potentielle svagheder.

- **Analyse af angrebsfladen:**

  Undersøgelse af målets teknologier, konfigurationer og potentielle indgangspunkter for at finde sårbarheder.

- **Indsamling af intelligens:**

  Opsamling af information, der kan bruges til yderligere angreb eller social engineering. Dette kan inkludere identificering af nøglepersoner, e-mailadresser eller mønstre i organisationens adfærd.

Angribere bruger disse oplysninger til at målrette angreb og omgå sikkerhedsforanstaltninger, mens forsvarere kan bruge dem til proaktivt at finde og lukke sårbarheder.

## To metoder inden for Web Reconnaissance
Web reconnaissance kan udføres på to måder: Aktiv rekognoscering og Passiv rekognoscering. Begge har deres styrker og svagheder.

## Aktiv Rekognoscering
Ved aktiv rekognoscering interagerer man direkte med målsystemet for at indsamle oplysninger. Dette kan være effektivt, men det indebærer også højere risiko for at blive opdaget.

| Teknik              | Beskrivelse                                                        | Eksempel                                                                    | Værktøjer                           | Opdagelsesrisiko |
| ------------------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------- | ----------------------------------- | ---------------- |
| Portscanning        | Identificer åbne porte og tjenester.                               | Brug af Nmap til at scanne porte som 80 (HTTP) og 443 (HTTPS).              | Nmap, Masscan                       | Høj              |
| Sårbarhedsscanning  | Afprøv kendte sårbarheder.                                         | Brug af Nessus til at finde SQL-injektionsfejl i en webapplikation.         | Nessus, OpenVAS, Nikto              | Høj              |
| Netværkskortlægning | Kortlægning af netværkets topologi.                                | Brug af traceroute til at finde netværkshop til målets server.              | Traceroute, Nmap                    | Medium til høj   |
| Banner grabbing     | Indsamling af oplysninger fra tjenester, fx serverbanner.          | Brug af Netcat til at finde versionsoplysninger om en webserver.            | Netcat, curl                        | Lav              |
| OS Fingerprinting   | Identifikation af operativsystem.                                  | Brug af Nmap til at finde ud af, om serveren kører Windows eller Linux.     | Nmap, Xprobe2                       | Lav              |
| Service Enumeration | Identifikation af versionsoplysninger for tjenester på åbne porte. | Brug af Nmap til at opdage, om en webserver kører Apache eller Nginx.       | Nmap                                | Lav              |
| Web Spidering       | Automatisk kortlægning af websider og filer.                       | Brug af Burp Suite Spider til at finde skjulte ressourcer på en hjemmeside. | Burp Suite Spider, OWASP ZAP Spider | Lav til medium   |

Aktiv rekognoscering giver dyb indsigt, men risikerer at udløse alarmer, da interaktion med målet ofte kan spores.

## Passiv Rekognoscering
Passiv rekognoscering indebærer, at man indsamler oplysninger uden direkte at interagere med målet. I stedet benyttes offentligt tilgængelige data.

| Teknik                    | Beskrivelse                                                           | Eksempel                                                                 | Værktøjer                      | Opdagelsesrisiko |
| ------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------ | ------------------------------ | ---------------- |
| Søgemaskine-forespørgsler | Brug af søgemaskiner til at finde information.                        | Søg på Google efter "[Mål] medarbejdere" for at finde sociale profiler.  | Google, DuckDuckGo, Shodan     | Meget lav        |
| WHOIS-opslag              | Find domæneregistreringsoplysninger.                                  | Brug af WHOIS til at finde ejerskab af et domæne.                        | whois-værktøjer, online opslag | Meget lav        |
| DNS-analyse               | Undersøgelse af DNS-poster for at finde underdomæner og mailsystemer. | Brug af dig til at finde DNS-poster for et mål.                          | dig, nslookup, dnsrecon        | Meget lav        |
| Webarkivanalyse           | Undersøgelse af historiske versioner af en hjemmeside.                | Brug af Wayback Machine til at se tidligere udgaver af en hjemmeside.    | Wayback Machine                | Meget lav        |
| Sociale medier-analyse    | Saml data fra platforme som LinkedIn eller Twitter.                   | Søg på LinkedIn efter nøglepersoner i organisationen.                    | LinkedIn, OSINT-værktøjer      | Meget lav        |
| Kodearkiver               | Analyse af offentligt tilgængelige kodearkiver, fx GitHub.            | Søg på GitHub efter kode relateret til målet, der kan afsløre svagheder. | GitHub, GitLab                 | Meget lav        |

Passiv rekognoscering er mere diskret og mindre risikofyldt, men kan være mindre detaljeret, da den kun anvender offentlige kilder.

Begge metoder er afgørende for en grundig forståelse af målet, og de bruges ofte i kombination for at opnå det bedste resultat.
