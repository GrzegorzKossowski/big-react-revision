<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>

# useContext

`const ThemeContext = createContext(defaultValue);`

`const value = useContext(SomeContext)`

Pozwala zasubskrybować lub czytać kontekst w danym komponencie

- pobiera dane z providera ponad sobą w drzewie
- jeśli nie znajdzie wartości, ustawia defaultową
- provider musi być tym samym obiektem!
- react rerenderuje komponent, jeśli zmieni sie kontekst, nawet jeśli komponent jest w `memo()`

## Context file
- pobiera jakieś api
- tworzy kontekst
- tworzy providera który opakowuje dzieci
- zwraca hooka, który zwraca wartość kontekstu

```js
// src/contexts/TodoContext.jsx
import { createContext, useContext } from "react";
import useFetchApi from "../hooks/useFetchState";

const TodoContext = createContext();

export function TodoProvider({ children }) {
  const { data, loading, error } = useFetchApi();

  // tu operacje lub dodatkowe funkcje do przekazania

  return (
    <TodoContext.Provider value={{ data, error, loading }}>
      {children}
    </TodoContext.Provider>
  );
}

export function useTodoContext() {
  return useContext(TodoContext);
}
```

## Provider file
- zaciąga kontekst providera
- przekazuje mu dzieci

```javascript
// src/App.jsx
import { TodoProvider } from "./contexts/todoContext";

function App() {
  return (
    <TodoProvider>
      <SomeProvider>
        {/* tu dalsze providery lub reszta aplikacji, dzieci, itp. */}
      </SomeProvider>
    </TodoProvider>
  );
}

export default App;
```

## Context user

- pobiera dane z kontekstu providera znadującego się powyżej w drzewie

```js
// src/components/component
import { useTodoContext } from "../contexts/todoContext";

function Todo() {
  const { data } = useTodoContext();

  return (
    <ul>
      {data.slice(0, 15).map((todo) => (
        <li key={todo.id}>
          <p>{todo.title}</p>
        </li>
      ))}
    </ul>
  );
}

export default Todo;
```

## Zmiana kontekstu

- zmiany wartości kontekstu można kontrolować przez kontrolę statnu na poziomie providera
- można przekazać 
  * wartość, 
  * obiekt,
  * zastosować kilka oddzielnych providerów dla każdej wartości
  * wydzielić zbiór providerów do oddzielnego komponentu
  * połączyć useContext z useReducer celem obsługi złożonego obiektu

```js
function MyPage() {
  const [theme, setTheme] = useState('dark');
  return (
    <ThemeContext.Provider value={{theme, setTheme}}>
    //...
  )}
```

## Optymizacja

- przekazując bardziej złożone obiekty, np. funkcje lub wartości, można je opakować wcześniej w `useCallback()` i `useMemo()`

<br/>
<br/>
<br/>

<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>
<a href='#top' style='border: 1px solid gold; padding: 5px; color: gold'>↑ back to top</a>
