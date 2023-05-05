<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>

# memo

`const MemoizedComponent = memo(SomeComponent, arePropsEqual?)`

Pozwala na pominięcie renderowania komponentu, jeśli jego propsy się nie zmieniły, nawet jeśli parent jest rerenderowany.
UWAGA: to optymalizacja, więc nie jest gwarantowana.

- aktualizuje komponent używając stanu lub kontekstu
- zmniejsza zmiany propsów
- często używany z useCallback.
- pozwala na ustawienie funkcji porównującej rerendery (nie stosowana)

Zwraca nowy komponent, ale niekoniecznie go rerenderuje, jeśli rerenderuje się parent.

```js
import { memo } from 'react';

const SomeComponent = memo(function SomeComponent(props) {
  // ...
});
```

## Zastosowanie

- do zastosowania w przypadku komponentów rzadko zmieniających swój stan
- częste zmiany propsów wykluczają sens użycia `memo`


<br/>
<br/>
<br/>

<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>
<a href='#top' style='border: 1px solid gold; padding: 5px; color: gold'>↑ back to top</a>
