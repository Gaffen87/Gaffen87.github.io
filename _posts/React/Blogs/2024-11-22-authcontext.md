---
layout: post
title: Implementering af authContext
date: 2024-11-22 14:31 +0000
categories: [React, React/blog]
image: assets/authcontext.png
---

## Oprettelse af AuthContext

``` jsx
const AuthContext = createContext({ user: null });
``` 

- createContext opretter en kontekst, som vil blive brugt til at dele brugerdata (f.eks. om en bruger er logget ind eller ej).
- Konteksten indeholder en standardværdi { user: null }, hvilket betyder, at der ikke er nogen bruger logget ind som udgangspunkt.

## AuthProvider-komponenten

AuthProvider er en komponent, som giver AuthContext adgang til hele React-applikationen.

- State og variabler:

``` jsx
const [user, setUser] = useState(null);
const [session, setSession] = useState(null);
const [loading, setLoading] = useState(true);
```

- **user:** Holder information om den loggede bruger (eller null, hvis ingen er logget ind).
- **session:** Holder Supabase-sessionen.
- **loading:** Angiver, om autentifikationsdata stadig indlæses.

## Brugerens session overvåges

``` jsx
useEffect(() => {
  const { data: listener } = supabase.auth.onAuthStateChange(
    (event, session) => {
      setSession(session);
      setUser(session?.user ?? null);
      setLoading(false);
    }
  );
  return () => {
    listener?.subscription.unsubscribe();
  };
}, []);
```

- **onAuthStateChange:** Supabase overvåger ændringer i autentifikationstilstanden (f.eks. login eller logout).
- Når en ændring sker:
  - Opdateres session med den nyeste session.
  - user opdateres med brugerdata, eller null, hvis der ikke er en bruger.
  - loading sættes til false, når ændringen er behandlet.
- **Cleanup:** Når komponenten fjernes fra DOM'en, afmeldes event-lytteren for at undgå hukommelseslækager.

## Sign In-funktionen

``` jsx
const signIn = async (username, password) => {
  setLoading(true);
  const email = await findUserEmail(username);
  const { data, error } = await supabase.auth.signInWithPassword({
    email,
    password,
  });
  setLoading(false);
  return { data, error };
};
```

- Brugeren logger ind med et brugernavn og en adgangskode.
- Supabase håndterer login med signInWithPassword, og den returnerer data eller fejl afhængigt af resultatet.
- loading bruges til at angive, at login-processen er aktiv.

## Sign Out-funktionen

``` jsx
const signOut = async () => {
  setLoading(true);
  const { error } = await supabase.auth.signOut();
  if (!error) {
    setUser(null);
    setSession(null);
  }
  setLoading(false);
  return { error };
};
```

- Logger brugeren ud via Supabase.
- Hvis det lykkes, nulstilles user og session til null.
- Fejl returneres, hvis logout mislykkes.

## Rendering af child components vs. loading-state

  {% raw %}
``` jsx
return (
  <AuthContext.Provider value={{ user, signIn, signOut }}>
    {!loading ? (
      children
    ) : (
      <IconContext.Provider value={{ size: "2em" }}>
        <div className="w-full h-dvh text-center flex items-center justify-center">
          <ImSpinner2 className="animate-spin" />
        </div>
      </IconContext.Provider>
    )}
  </AuthContext.Provider>
);
```
      {% endraw %}

- AuthContext.Provider gør det muligt for underliggende komponenter at bruge user, signIn, og signOut.
- Hvis loading er true, vises en spinner, der angiver, at applikationen stadig venter på brugerens autentifikationsstatus.
- Når loading er false, gengives child components (children).

## Custom Hook til AuthContext

``` jsx
export const useAuth = () => {
  return useContext(AuthContext);
};
```

Et custom hook, der gør det nemt at bruge AuthContext i andre komponenter:

``` jsx
const { user, signIn, signOut } = useAuth();
```

## Anvendelse
AuthProvider bruges som en "wrapper" omkring applikationen i fx. App.js:

``` jsx
<AuthProvider>
  <App />
</AuthProvider>
```

I andre komponenter kan du bruge useAuth til at få adgang til brugerdata og autentifikationsfunktionalitet:

``` jsx
const { user, signIn, signOut } = useAuth();

if (user) {
  console.log("Bruger logget ind:", user);
} else {
  console.log("Ingen bruger logget ind.");
}
```
