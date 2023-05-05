<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>

# createContext

`const SomeContext = createContext(defaultValue)`

Tworzy kontekst, który komponenty mogą dostarczać lub czytać. Pozwala na przekazanie danych w dół drzewa komponentów.
Tworzymy go poza komponentem, np. jako osobny moduł.

```js
import { createContext } from 'react';

// kontekst z defaultową wartością null
const ThemeContext = createContext(null);

// kontekst z defaultową wartością 'light'
const ThemeContext = createContext('light');
```

- wartość defaultowa nie zmienia się, jest statyczna, jest używana, jeśli żaden kontekst nie dostarczy innej zmiennej.

## SomeContext.Provider

Komponent udostępniający kontekst w drzewie potomków.

```html
<ThemeContext.Provider value={theme}>
    //...
</ThemeContext.Provider>
```

## SomeContext.Consumer? - useContext()

Aktualnie nieużywany. Obecnie używany jest hook `useContext()`.

```js
  const theme = useContext(ThemeContext);
  return <button className={theme} />;
```

## Zastosowanie

Przykład wykorzystania: <a href='./useContext.md'>useContext.md</a>

<br/>
<br/>
<br/>

<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>
<a href='#top' style='border: 1px solid gold; padding: 5px; color: gold'>↑ back to top</a>
