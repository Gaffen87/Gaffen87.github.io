---
layout: post
title: Testing i React
date: 2024-11-12 13:19 +0000
categories: [React, React/blog]
image: https://media.daily.dev/image/upload/f_auto,q_auto/v1/posts/0e80f7a6fea2e19e50ff2b4401adb81a
---

## Test af React komponenter med Vitest og React Testing Library

### For at udføre tests har vi brug for følgende pakker:

- **Vitest:** Test framework.
- **JSDOM:** Simulerer DOM i tests.
- **React Testing Library:** Testværktøjer specifikt til React.

### Installer disse med:

``` bash
yarn add -D vitest jsdom @testing-library/react
```

### Konfiguration af Vitest

I filen vite.config.js tilføjes en test-konfiguration:

``` javascript
export default defineConfig({
  test: {
    global: true,
    environment: 'jsdom',
  },
});
```

- global: Gør testmetoder tilgængelige uden yderligere import.
- environment: Angiver, at testen skal køre i en "jsdom"-miljø.

Tilføj desuden et test-kommando til package.json:

``` json
"scripts": {
  "test:unit": "vitest --root src/"
}
```

### Udvidelse af expect med DOM-metoder

For at få metoder som `toBeInTheDocument()` og `toHaveTextContent()` til DOM-elementer, skal du installere pakken:

``` bash
yarn add -D @testing-library/jest-dom
``` 

Opret derefter en fil setupTest.js i projektets rodkatalog, og tilføj følgende:

``` javascript
import { expect } from 'vitest';
import matchers from '@testing-library/jest-dom/matchers';

expect.extend(matchers);
```

Til sidst registreres denne fil i vite.config.js under feltet setupFiles:

``` javascript
test: {
  setupFiles: './setupTest.js',
}
``` 

### Eksempel på test af en React-komponent

Vi tester en komponent kaldet Movies, der viser en liste af film og har søgefunktion.

Movies-komponentens kode:

``` javascript
export const Movies = () => {
  const { movies } = useMovies();
  const { searchTerm, setSearchTerm, filteredItems: filteredMovies } = useSearch(movies);
  
  return (
    <section>
      <div>
        <label htmlFor="search">Search</label>
        <input
          type="search"
          id="search"
          value={searchTerm}
          data-testid="search-input-field"
          onChange={(event) => setSearchTerm(event.target.value)}
        />
      </div>
      <ul data-testid="movies-list">
        {filteredMovies.map((movie, index) => (
          <li key={index}>
            <article>
              <h2>{movie.title}</h2>
              <p>Release on: {movie.release_date}</p>
              <p>Directed by: {movie.director}</p>
              <p>{movie.opening_crawl}</p>
            </article>
          </li>
        ))}
      </ul>
    </section>
  );
};
```

### Testopsætning

Vi bruger `vi.spyOn()` fra Vitest til at overvåge og mocke hooks useMovies og useSearch:

``` javascript
import * as useMoviesHooks from '../hooks/useMovies';
import * as useSearchHooks from '../hooks/useSearch';

describe('Movies', () => {
  const useMoviesSpy = vi.spyOn(useMoviesHooks, 'useMovies');
  const useSearchSpy = vi.spyOn(useSearchHooks, 'useSearch');
});
```

Mock værdierne returneres som:

``` javascript
useMoviesSpy.mockReturnValue({ movies: items });
useSearchSpy.mockReturnValue({
  searchTerm: '',
  setSearchTerm: vi.fn(),
  filteredItems: items,
});
``` 

### Testrendering

Renderer komponenten og verificerer, at listen over film vises korrekt:

``` javascript
import { render, screen } from '@testing-library/react';
import { Movies } from './Movies';

it('should render the list of movies', () => {
  const { getByTestId } = render(<Movies />);
  expect(getByTestId('movies-list').children.length).toBe(items.length);
});
```

### Test af søgefunktion

For at teste søgefeltet bruger vi:

- fireEvent.change() til at simulere inputændringer.
- act() for at sikre, at ændringerne reflekteres korrekt i DOM'en.

``` javascript
import { act, fireEvent } from '@testing-library/react';

it('should change the filtered items when the search term changes', () => {
  const { getByTestId } = render(<Movies />);
  const searchInput = getByTestId('search-input-field');
  
  act(() => {
    fireEvent.change(searchInput, { target: { value: 'Wars' } });
  });

  expect(getByTestId('movies-list').children.length).toBe(1);
});
```

### Oprydning

For at sikre isolerede tests ryddes mocks og DOM efter hver test:

``` javascript
afterEach(() => {
  useMoviesSpy.mockClear();
  useSearchSpy.mockClear();
});

import { cleanup } from '@testing-library/react';

afterEach(() => {
  cleanup();
});
```
