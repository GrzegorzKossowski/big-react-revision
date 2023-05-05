<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>

# lazy

`const SomeComponent = lazy(load)`

Ogranicza ładowanie komponentu do czasu pierwszego wykorzystania.

- nie pobiera komponentu, jeśli nie jest potrzebny
- ogranicza zużycie transferu
- zapewnia bezpieczeństwo, nie ładuje kodu, jeśli nie ma dostępu do komponentu
- używa dynamiczneg ładowania, co wymaga działającej obsługi tego w stosowanym bundlerze
- wymaga deklaracji w module, nie komponencie!

## Zastosowanie

```js
import { lazy } from 'react';

const MarkdownPreview = lazy(() => import('./MarkdownPreview.js'));
```

Lazy lodading wymaga opakowania w `Suspense`.

```html
<Suspense fallback={<Loading />}>
  <h2>Preview</h2>
  <MarkdownPreview />
 </Suspense>
 ```



<br/>
<br/>
<br/>

<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>
<a href='#top' style='border: 1px solid gold; padding: 5px; color: gold'>↑ back to top</a>
