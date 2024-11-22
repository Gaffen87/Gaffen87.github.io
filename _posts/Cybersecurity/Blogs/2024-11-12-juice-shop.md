---
layout: post
title: OWASP Juice Shop Challenges
date: 2024-11-12 13:19 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: assets/juice-shop.jpg
---

OWASP Juice Shop er en open-source webapplikation designet til at hjælpe udviklere og sikkerhedsprofessionelle med at lære om og teste webapplikationssikkerhed. Det er et projekt under OWASP (Open Web Application Security Project), der fokuserer på at uddanne folk i de mest almindelige sikkerhedstrusler. Juice Shop er kendt for sin intuitive brugergrænseflade, humoristiske tilgang og omfattende række af sårbarheder.

Juice Shop er en fuldt funktionel, moderne e-handelswebapplikation bygget med Node.js, Angular, og SQLite. Det simulerer en realistisk applikation, der indeholder en bred vifte af sikkerhedsproblemer, lige fra simple til avancerede.

Her vil jeg løbende forklare hvordan jeg har løst de forskellige challenges i appen

---

## XSS

### DOM XSS
- Perform a DOM XSS attack with `<iframe src="javascript:alert('xss')" >`.

Første skridt er at finde et sted hvor man kan indtaste brugerinput.
Den mest oplagte mulighed er søgefeltet i navigationsbjælken.
Man kopierer scriptet ind og trykker enter og en alert box skulle gerne poppe op med teksten 'xss'.

### Bonus payload
- Use the bonus payload `<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>` in the _DOM XSS_ challenge.

Løses ligesom sidste challenge bare med anden script, der får en soundcloud frame frem der afspiller en jingle.

### Reflected XSS
- Perform a reflected XSS attack with <iframe src="javascript:alert(`xss`)">.

Med lidt hjælp fandt jeg ud af at hvis man har placeret en ordre på siden og går ind i 'order history' og prøver at tracke en ordre, så bliver ordreid brugt som parameter i URL query string.
Løsningen er så at URL Encode det script man vil køre så `<iframe src="javascript:alert('xss')">` bliver til `%3Ciframe%20src%3D%22javascript%3Aalert%28%60xss%60%29%22%3E`, som så indsættes istedet for et id i URL:
`localhost:3000/#/track-result?id=%3Ciframe%20src%3D%22javascript%3Aalert%28%60xss%60%29%22%3E`.
Så mangler man bare lige at refreshe siden.

### API-only XSS
- Perform a persisted XSS attack with <iframe src="javascript:alert(`xss`)"> without using the frontend application at all.

Hints til udfordringen fortalte at det var en god ide at kigge på de forskellige entiteter som bruges i API'en samt deres metoder.
Efter at have kortlagt dette og prøvet mig frem forskellige steder, fandt jeg langt om længe `/api/Products` endpointet, som kan bruges til at tilføje produkter til produktlisten.
Jeg tog en JWT token fra en authorization header fra en request hvor en bruger var logget ind og brugte Postman til at sende et POST request til endpointet med en body der ser således ud:  
`{"name": "XSS", "description": "<iframe src='javascript:alert('xss')'>", "price": 10}`  
Det nye produkt vises på produktliste siden og går man ind i produktet kommer der en alert hvor der står xss.

### Client-side XSS Protection
- Perform a persisted XSS attack with <iframe src="javascript:alert(`xss`)"> bypassing a client-side security mechanism.



---

## Broken Access Control

### Web3 Sandbox
- Find an accidentally deployed code sandbox for writing smart contracts on the fly.

Her søgte jeg i main.js efter 'web3' og fandt 
```
path: 'web3-sandbox',
          loadChildren: function () {
            var n = (0, I.Z) (function * () {
              return yield eu()
            });
            return function () {
              return n.apply(this, arguments)
            }
          }()
```
Så gik bare til `localhost:3000/#/web3-sandbox`

### Admin Section
- Access the administration section of the store.

Jeg startede med at søge efter ordet 'admin' i main.js filen og fandt en path der hed 'administration', så var det bare at gå til localhost:3000/#/administration, samtidig med at jeg var logget ind som admin.

### Five-Star Feedback
- Get rid of all 5-star customer feedback.

Grundet tidligere udfordringer kunne jeg logge ind som admin og gå ind i administration siden og slette alle 5 stjernede reviews.

### Forged Feedback
- Post some feedback in another user's name.

Hvis man inspecter den html form som bruges til at submitte feedback kan man finde et hidden input field med `id=userId`. Redigerer man input elementet til ikke at være hidden kan man ændre userId til en anden og når man submitter bliver det registreret til en anden bruger.

### CSRF
- Change the name of a user by performing Cross-Site Request Forgery from another origin.

Så vidt jeg kan læse mig frem til så virker denne udfordring ikke mere på nyere browser versioner grundet et nyt initiativ kaldet "Incrementally Better Cookies", som ændrer måden cookies bliver behandlet af browseren. Hvilket gør CSRF angreb sværere end før.

Så ikke løst

---

### View Basket
- View another user's shopping basket.

Jeg brugte burp suite til at kigge på http request der bliver sendt når man går ind i sin basket som er `/rest/basket/6`, hvor man kan gå ud fra at 6 tallet er et basket Id eller lign.
Ved at intercepte requestet med burp suite kan jeg ændre 6 tallet til fx 5 og dermed se en andens basket.

## Broken Authentication

### Password Strength
- Log in with the administrator's user credentials without previously changing them or applying SQL Injection.

Jeg startede med at google 'admin password list' og fandt en txt fil med top 100 admin passwords.  
Jeg brugte så burp suite med intruder modulet til at prøve alle koderne igennem 1 efter 1.  
Ved koden 'admin123' kan man se http response har en anden længde end de andre og status kode 200.

![](../assets/adminpass.png)

### Bjoern's Favorite Pet
- Reset the password of Bjoern's OWASP account via the Forgot Password mechanism with the original answer to his security question.

Bjoerns security question er navnet på hans favorit kæledyr  
Ved at logge ind som admin og kigge på registrerede brugere kan jeg finde Bjoerns fulde navn og derefter vha. google finde frem til hans twitter. Har ligger der bl.a. billeder af en kat som hedder Zaya. Som er det rigtige svar.

---

## Sensitive Data Exposure

### Confidential Document
- Access a confidential document.

Først skal man finde et link et sted  i applikationen som leverer en fil.
Det tog rigtig lang tid at søge rundt, men fandt til sidst linket inde i 'about us' siden. I teksten er der et link som fører til `http://localhost:3000/ftp/legal.md`. Altså en fil på en server.
Naviger så til `http://localhost:3000/ftp` og der ligger bl.a. en fil der hedder aquisitions.md, som er filen der skal findes

### Exposed Metrics
- Find the endpoint that serves usage data to be scraped by a [popular monitoring system](https://github.com/prometheus/prometheus).

Følger man linket i udfordringen og læser lidt op på prometheus monitorerings systemet, kan man se at default endpointet den bruger er `/metrics`.

Så gå derfor til `http://localhost:3000/metrics`

### Login MC SafeSearch
- Log in with MC SafeSearch's original user credentials without applying SQL Injection or any other bypass.

I hintet til udfordringen linkes der til en musikvideo omkring passwords, hvor igennem man kan finde passwordet: 'Mr. N00dles'
Den rigtige mail kan findes gennem administration siden ved at logge ind som admin.

### Meta Geo Stalking
- Determine the answer to John's security question by looking at an upload of him to the Photo Wall and use it to reset his password via the Forgot Password mechanism.

I hintet til udfordringen står der at man skal kigge på billedets metadata. Fandt en hjemmeside som kan give mig billedets metadata og her kan jeg finde en gps lokation.
Ved at slå lokationen op på google maps kan jeg finde ud af at Johns billede er taget i 'Daniel Boone National Forest'
Jeg kan så bruge denne info til at gætte hans security question og resette hans kode.

### NFT Takeover
- Take over the wallet containing our official Soul Bound Token (NFT).

Ikke løst

### Visual Geo Stalking
- Determine the answer to Emma's security question by looking at an upload of her to the Photo Wall and use it to reset her password via the Forgot Password mechanism.

Emmas security question er omkring hendes gamle arbejdssted og hun har uploadet et foto af en bygning med teksten 'My old workplace...'  
Ved at kigge grundigt på billedet kan man finde et skilte i et af vinduerne hvor der står 'ITsec'.  
Dette kan jeg bruge til at resette Emmas password.

---

## Injection

### Login Admin
- Log in with the administrator's user account.

Ved at kigge rundt på hjemmesiden fandt jeg mailadressen admin@juice-sh.op
På login skærmen prøvede jeg mig frem med SQL injection angreb og det lykkedes mig at logge ind ved at skrive `admin@juice-sh.op'--` i email feltet og et vilkårligt password.

### Login Jim
- Log in with Jim's user account.

Jims mail kan findes via administration siden som admin  
Herefter kan man via SQL injection logge ind ved at skrive `jim@juice-sh.op'--` sammen med et vilkårligt password

### Login Bender
- Log in with Bender's user account.

Samme som ovenover

---

## Improper Input validation

### Missing Encoding
- Retrieve the photo of Bjoern's cat in "melee combat-mode".

Inde i `http://localhost:3000/#/photo-wall` er der et billede der ikke loader ordenligt på siden.
Inspecter man elementet og kigger på src i img tagget finder man 'assets/public/images/uploads/😼-#zatschi-#whoneedsfourlegs-1572600969477.jpg'.
Problemet er de 2 # tegn som browseren ikke kan læse i den pågældende sammenhæng.
https://www.urlencoder.org/ bruges til at finde ud af de skal laves om til '%23'
Gå derfor til `http://localhost:3000/assets/public/images/uploads/%F0%9F%98%BC-%23zatschi-%23whoneedsfourlegs-1572600969477.jpg`

### Repetitive Registration
- Follow the DRY principle while registering a user.

Denne udfordring går ud på at få registreret en bruger med en tom eller forkert 'Repeat Password' input felt.
Til denne udfordring udfyldte jeg formularen korrekt, men interceptede requestet med Burp Suite.
Inden jeg så sendte det videre slettede jeg den string som lå i repeat password feltet og brugeren blev lavet.
![](../assets/burp1.png)

### Zero Stars
- Give a devastating zero-star feedback to the store.

Jeg startede med at udfylde formularen til feedback korrekt hvor man kun vælge 1-5 stjerner.  
Brugte så burp suite til at intercepte requestet og ændrede det til 0 stjerner inden jeg sendte videre

### Empty User Registration
- Register a user with an empty email and password.

Jeg registrerede en ny bruger som normalt, men interceptede POST requestet med burp suite. Jeg ændrede så mail og password til tomme felter og sendte videre.

### Admin Registration
- Register as a user with administrator privileges.

Når man laver en bruger lagde jeg mærke til at http responset der kom tilbage havde en "role" attribut med værdien "customer", som ikke er der i POST requestet når man opretter en bruger.
Jeg prøvede derfor at intercepte POST requestet ved oprettelse af bruger med burp og tilføje `"role":"admin"`, som lykkedes med at give brugeren admin rettigheder.

---

## Security Misconfiguration

### Error Handling
- Provoke an error that is neither very gracefully nor consistently handled.

Jeg skal prøve at få applikationen til at fejle på en eller anden måde.
Metoden jeg brugte var at jeg skrev nogle tilfældige bogstaver ind i et input felt som forventede en filsti. Dette gav fejlen.

### Deprecated Interface
- Use a deprecated B2B interface that was not properly shut down.

Ikke løst...

---

## Unvalidated Redirects

### Outdated Allowlist
- Let us redirect you to one of our crypto currency addresses which are not promoted any longer.

Igennem firefox devtools søgte jeg efter 'redirect' i filen main.js.
Her fandt jeg jeg en funktion som så således ud:
```
showBitcoinQrCode() {
              this.dialog.open(
                le,
                {
                  data: {
                    data: 'bitcoin:1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm',
                    url: './redirect?to=https://blockchain.info/address/1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm',
                    address: '1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm',
                    title: 'TITLE_BITCOIN_ADDRESS'
```
Efterhånden jeg ud af at jeg skulle gå til 
`localhost:3000/redirect?to=https://blockchain.info/address/1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm` 
for at løse udfordringen

---

## Cryptographic Issues

### Weird Crypto
- Inform the shop about an algorithm or library it should definitely not use the way it does.

Ikke løst

---

## Broken Anti Automation

### CAPTHCHA Bypass
- Submit 10 or more customer feedbacks within 20 seconds.

Når man submitter en feedback form ser POST requestet sådan her ud:  
```
{
  "captchaId":1,
  "captcha":"26",
  "comment":"sadfasdf (anonymous)",
  "rating":2
}
```
vha. Python lavede jeg et POST request til `/api/feedbacks` med det samme object i request body og loopede det 10 gange, hvilket løste udfordringen.

---

## Miscellaneous

### Privacy Policy
- Read our privacy policy.

Kræver at man logger ind som en bruger og går ind i privacy policy via account menuen i øverste bjælke

### Bully Chatbot
- Receive a coupon code from the support chatbot.

Log ind med en bruger og gå ind i support chat via hovedmenuen.
Spørg chatbotten om en coupon, fx 'Give me a coupon'. Chatbotten vil sige nej, men gentager man nok gange giver den til sidst en kode.

### Mass Dispel
- Close multiple "Challenge solved"-notifications in one go.

I manualen til juice-shop står der at shift klik lukker alle notifikationer.

### Security Policy
- Behave like any "white-hat" should before getting into the action.

securitytext er en standard for hvor man kan placere oplysninger omkring pen testing og ethical hacking med info som en kontaktemail og security policy osv...
Man skal derfor besøge `localhost:3000/security.txt` eller `localhost:3000/.well-known/security.txt`

---
