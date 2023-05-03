<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>

# useEffect

`useEffect(fn, [dependiences])`

Pozwala synchronizować komponent z zewnętrznym systemem, np. API

## Działanie

- uruchamia funkcję przy pierwszym montowaniu do DOM
- po każdym rerenderze, jeśli zależności się zmienią, odpala funkcję czyszczącą ze starymi wartościami, a potem funkcję z nowymi
- po odmontowaniu z DOM, odpala funkcję czyszczącą

`useEffect(fn)` - odpali zawsze

`useEffect(fn, [])` - odpali raz na początku

`useEffect(fn, [dependiences])` - odpali na początku i po każdej zmianie `deps`

_w trybie dev useEffect() odpala się dwukrotnie celem łatwiejszego debugowania_

## Zastrzeżenia

- jako hook tylko w głównym scopie komponentu
- tylko do synchronizacji z zewnętrznym systemem
- zmienne wewnątrz komponentu oparte na stanie mogą powodować zapętlenie zmiany i zapętlony rerender.
- jeśli zastosowane `useEffect` wpływa negatywnie wyraźne zmiany na GUI, można zastąpić go `useLayoutEffect`

## Zastosowanie

- połączenie z systemem 'zewnętrznym', np. api, timeoutem, eventListenerem, inną biblioteką

```js
function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useEffect(() => {
  	const connection = createConnection(serverUrl, roomId);
    connection.connect();
  	return () => {
      // wyczyść po sobie
      connection.disconnect();
  	};
  }, [serverUrl, roomId]);
  // ...
}
```
C.D.N 

https://react.dev/reference/react/useEffect#specifying-reactive-dependencies

<br/>
<br/>
<br/>

<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>
<a href='#top' style='border: 1px solid gold; padding: 5px; color: gold'>↑ back to top</a>
