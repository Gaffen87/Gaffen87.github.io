---
layout: post
title: React og Supabase
date: 2024-11-12 13:20 +0000
categories: [React, React/blog]
image: assets/supabase.png
---

Supabase er en open-source backend-as-a-service (BaaS), der giver udviklere mulighed for hurtigt at bygge moderne applikationer med en robust og skalerbar backend. Det fungerer som et alternativ til Firebase, men er bygget på åbne teknologier som PostgreSQL og tilbyder funktioner til databasehåndtering, autentifikation, lagring og realtidsfunktioner.

Supabase er designet til at gøre backend-udvikling enklere og mere tilgængelig ved at kombinere kraftfulde teknologier med et brugervenligt interface og en moderne udvikleroplevelse.

I vores projekt har vi valgt at bruge supabase som auth-løsning, da det er forholdsvist simpelt og hurtigt at sætte op og bruge.

Supabase kan opsættes til react via deres javascript library:
`npm install @supabase/supabase-js`  

Herefter opretter man en supabase klient i sin kode:
```
import { createClient } from '@supabase/supabase-js';

const SUPABASE_URL = 'https://navnpåsupabaseorganisation.supabase.co';
const SUPABASE_ANON_KEY = 'public-anon-key';

export const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
```  

Her er et hurtigt eksempel på hvordan login kan se ud i React:
```
import React, { useState } from 'react';
import { supabase } from './supabaseClient';

const Auth = () => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [message, setMessage] = useState('');

  const handleLogin = async (e) => {
    e.preventDefault();
    const { error } = await supabase.auth.signInWithPassword({
      email,
      password,
    });

    if (error) {
      setMessage('Fejl ved login: ' + error.message);
    } else {
      setMessage('Login vellykket!');
    }
  };

  return (
    <div>
      <h1>Log ind</h1>
      <form onSubmit={handleLogin}>
        <input
          type="email"
          placeholder="E-mail"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
        />
        <input
          type="password"
          placeholder="Adgangskode"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
        />
        <button type="submit">Log ind</button>
      </form>
      <p>{message}</p>
    </div>
  );
};

export default Auth;
```
