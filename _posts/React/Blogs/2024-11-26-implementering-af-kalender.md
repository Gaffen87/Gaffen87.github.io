---
layout: post
title: Implementering af kalender
date: 2024-11-26 12:56 +0000
categories: [React, React/blog]
image: assets/reactbigcalendar.png
---

Til at bygge en kalenderfunktion til projektet, valgte vi at bruge "React Big Calendar". Det er et kraftfuldt værktøj, der giver mulighed for at håndtere tidsplanlægning, begivenheder og ressourcestyring. Her vil jeg gennemgå, hvordan jeg implementerede det, og hvilke overvejelser jeg gjorde mig undervejs.

## Opsætning af grundlæggende funktionalitet

Jeg startede med at installere React Big Calendar og Moment, som jeg brugte til dato- og tidsformatering. Dette gør det nemt at tilpasse kalenderen til en dansk kontekst.

``` bash
npm install react-big-calendar moment
``` 

I koden importerede jeg de nødvendige biblioteker og satte momentLocalizer op.  
Det var vigtigt for mig, at kalenderen kunne vises på dansk, så jeg tilpassede moment til danske måneder, ugedage og andre formatindstillinger:

```javascript
import moment from "moment";
import { momentLocalizer } from "react-big-calendar";

moment.updateLocale("da-DK", {
  months: ["Januar", "Februar", "Marts", "April", "Maj", "Juni", "Juli", "August", "September", "Oktober", "November", "December"],
  weekdays: ["Søndag", "Mandag", "Tirsdag", "Onsdag", "Torsdag", "Fredag", "Lørdag"],
  week: { dow: 1 }, // Ugen starter med mandag
});

const localizer = momentLocalizer(moment);
```

Ved at bruge localizer sørger jeg for, at kalenderens tids- og datoformater stemmer overens med danske standarder.

## Opsætning af Kalenderkomponenten

Jeg brugte komponenten `<Calendar />` som fundament for brugergrænsefladen. Den vigtigste del her var at definere de props, der styrer, hvordan kalenderen ser ud og fungerer.

Her er et eksempel på opsætningen af selve komponenten:

```javascript
import { Calendar } from "react-big-calendar";
import "react-big-calendar/lib/css/react-big-calendar.css";

<Calendar
  localizer={localizer}
  events={events} // Liste over begivenheder
  startAccessor="start" // Felt til starttidspunkt
  endAccessor="end" // Felt til sluttidspunkt
  views={["month", "day"]} // Tillad kun måneds- og dagsvisning
  defaultView="month" // Start med månedsvisning
  selectable // Tillad at vælge tidsrum
  onSelectEvent={(event) => setSelectedEvent(event)} // Håndter klik på en begivenhed
  onSelectSlot={(slot) => handleNewEvent(slot)} // Håndter valg af tidsrum
/>
```

Kalenderen blev opsat til at vise en liste over begivenheder fra en database. Events-prop'en var en nøglefunktion her, og jeg strukturerede begivenhederne som en liste af objekter, f.eks.:

```javascript
const events = [
  {
    id: 1,
    title: "Team-møde",
    start: new Date(2024, 10, 22, 10, 0), // 22. november kl. 10:00
    end: new Date(2024, 10, 22, 12, 0), // 22. november kl. 12:00
    allDay: false,
  },
];
```

## Hente begivenheder fra databasen

Jeg lavede en funktion, der indlæser begivenheder fra API'et og konverterer dem til et format, som React Big Calendar forstår:

```javascript
const fetchActivities = async () => {
  const { activities, error } = await getAllActivities(token);
  if (!error) {
    activities.forEach((activity) => {
      setEvents((prevEvents) => [
        ...prevEvents,
        {
          id: activity.id,
          start: new Date(activity.start),
          end: new Date(activity.end),
          title: activity.title,
          description: activity.description,
          allDay: activity.allDayEvent,
        },
      ]);
    });
  }
};
```

## Tilføje nye begivenheder

For at give brugerne mulighed for at oprette nye begivenheder lavede jeg en modal. Modal-komponenten lod dem udfylde titel, beskrivelse og tidsrum for begivenheden, og derefter blev oplysningerne gemt i databasen.

```javascript
const saveActivitytoDb = async () => {
  const token = await getSessionToken();
  const response = await createActivity(event, token);
  setEvents((prevEvents) => [...prevEvents, { ...event, id: response.id }]);
};
```

## Tilpasning af kalenderen
For at give brugerne en god oplevelse tilpassede jeg kalenderens udseende. For eksempel lavede jeg farvekodning for forskellige typer begivenheder og gjorde det tydeligt, hvis en begivenhed var aflyst:

```javascript
eventPropGetter={(event) => {
  if (event.cancelled) {
    return { style: { backgroundColor: "gray", textDecoration: "line-through", opacity: 0.5 } };
  }
  return { style: { backgroundColor: "blue" } };
}}
```

## Opsamling
Det, jeg især godt kan lide ved React Big Calendar, er dens fleksibilitet og indbyggede understøttelse af funktioner som drag-and-drop, forskellige visninger og integration med forskellige datoformateringsbiblioteker. Implementeringen var ikke altid ligetil, men heldigvis findes der en ok grundig dokumentation, som jeg benyttede mig flittigt af.
