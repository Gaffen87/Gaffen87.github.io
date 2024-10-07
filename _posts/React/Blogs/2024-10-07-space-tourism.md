---
layout: post
title: space-tourism React challenge
date: 2024-10-07 08:33 +0000
categories: [React, React/blog]
image: assets/space-tourism.png
---

# Space Tourism Challenge


[Link til min løsning af denne challenge](https://space-gaffen.netlify.app)
[Github](https://github.com/Gaffen87/space-tourism)

Jeg fandt denne udfordringen gennem [frontendmentor.io](https://www.frontendmentor.io/challenges/space-tourism-multipage-website-gRWj1URZ3), hvor der udleveres design filer og assets til at opbygge hjemmeside. Målet er at få den til at se ud som designet og lave interaktionen.

Jeg brugte øvelsen til at lære mere om React generelt og få noget praktisk erfaring med at bruge React Router. Derudover har jeg brugt Framer Motion til animationer og TailwindCSS til styling.

Jeg vil her forklare lidt om hvordan jeg har opsat hjemmesiden med React og brugen af React Router

Til læring om React Router har jeg prøvet så vidt muligt at holde mig til den officiele [dokumentation](https://reactrouter.com/en/main)

## Opsætning af React Router

Jeg brugte React Routers createBrowserRouter til at opsætte mine routes.
Hjemmesiden består bl.a. af en navigationsmenu, hvor der kan navigeres til forskellige sider.
![navbar](assets/spaceNavBar.png)

Derfor opsætter jeg 4 routes således:
``` jsx
const router = createBrowserRouter([
	{
		path: "/",
		element: <App />,
		children: [
			{
				path: "/",
				element: <Navigate to="home" replace />,
			},
			{
				path: "home",
				element: <Home />,
			},
			{
				path: "destinations",
				element: <Destinations />,
			},
			{
				path: "crew",
				element: <Crew />,
			},
			{
				path: "technology",
				element: <Technology />,
			},
		],
	},
]);
```

Her defineres de ønskede paths og deres tilhørende React Component
Min main path "/" består af elementet `<App />` og som ses i koden er de resterende routes sat ind som children til denne route
Med denne opsætning fungerer hjemmesiden som en SPA(Single Page Application), hvor mit main route element altid vises og de andre kan vises inde i det element alt efter hvilken route man er på.

Dette faciliteres i React Router med at bruge det indbyggede `<Outlet />` element.

`<App />` kommer derfor til at se nogenlunde sådan her ud:
``` jsx
<div className="h-dvh w-screen overflow-hidden bg-no-repeat bg-cover bg-black bg-center transition-all duration-1000 bg-fixed">
	<Navbar />
	<Outlet />
</div>
``` 

Her ses det at min side består af en Navbar og et outlet element der skiftes ud med det pågældende routes element

## NavBar links
Til at give brugeren mulighed for at navigere mellem de forskellige sider har React Router et indbygget `<Link />` element beskrevet således i den officiele dokumentation:
> A `<Link>` is an element that lets the user navigate to another page by clicking or tapping on it. In react-router-dom, a `<Link>` renders an accessible `'<a>'` element with a real href that points to the resource it's linking to. This means that things like right-clicking a `<Link>` work as you'd expect.

Elementet fungerer ved at men giver den et valgt path således: `<Link to={"path"}>Link text</Link>`

En lidt udvidet udgave findes i `<NavLink` elementet som fungerer på samme måde, men som ved om det er aktivt eller ikke. Dermed kan man vise brugeren hvilken side de er på pt. i navigations baren, ved fx at highlighte linket.

Jeg har opsat navigation via `<NavLink>` på følgende måde:
``` jsx
{navItems.map((key, index) => {
	return (
		<NavLink
			to={key}
			key={key}
			className="h-full gap-spacing-100 flex items-center cursor-pointer box-border border-y-4 border-y-transparent hover:border-opacity-50 hover:border-b-white transition-all duration-500"
		>
		  <span className="font-barlowCondensed leading-[19.2px] tracking-[2px] font-bold">
				0{index}
			</span>
			<span className="font-barlowCondensed leading-[19.2px] tracking-[2px]">
				{key.toUpperCase()}
			</span>
		</NavLink>
	);
})}
```
Dernæst kan jeg tilføje en simpel CSS klasse som styler linket hvis det er aktivt:
``` css
a.active {
	border-bottom-color: white;
}
```
![sdfsa](assets/navbargif.gif)

## Dynamiske baggrundsbilleder
Jeg rendte ind i en lille udfordring ift. at hver side skulle have sin egen baggrund der skiftede når man navigerede. Da baggrunden skulle fylde hele skærmen, var den nødt til at være sat i mit `<App />` hovedelement. Men hvordan skiftede jeg så baggrunden automatisk?

Til dette fandt en indbygget hook i React Router som hedder [useLocation()](https://reactrouter.com/en/main/hooks/use-location).

Hooket returnerer et location objekt som ser således ud:
![](assets/locationobject.png)

Her kan vi så udlede "pathname" som i dette tilfælde er lig "/destinations", hvilket er brugerens nuværende path på web siden.
Dette kunne jeg så concatenate ind i stien til baggrundsfilerne som var med i udfordringen

``` javascript
	let path = location.pathname.slice(1);
	if (path === "destinations") path = "destination";
	if (!path) {
		path = "home";
	}

	const desktopImageKey = `./assets/${path}/background-${path}-desktop.jpg`;
	const mobileImageKey = `./assets/${path}/background-${path}-mobile.jpg`;
```
...og dermed skiftede baggrunden til det rette billeder alt efter hvor brugeren navigerer hen!

