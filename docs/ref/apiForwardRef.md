<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>

# forwardRef

`const SomeComponent = forwardRef(render)`

Pozwala na ekspozycję nodea do parenta za pomocą `ref`.

-   Opakowuje komponent, który może przyjąć oprócz propsów także ref z parenta.

### Parent

```js
function Form() {
    // deklaruje ref
    const ref = useRef(null);

    // funkcja działająca na ref (tu, focus)
    function handleClick() {
        ref.current.focus();
    }

    return (
        <form>
            // przekazuje ref w głąd drzewa do dziecka i tam go zakotwicza
            <MyInput label='Enter your name:' ref={ref} />
            <button type='button' onClick={handleClick}>
                Edit
            </button>
        </form>
    );
}
```
### Child
```js
// pobiera ref w parametrach
const MyInput = forwardRef(function MyInput(props, ref) {
    return (
        <label>
            {props.label}
            // zakotwicza ref w elemencie dziecka, kontrolując go z poziomu rodzica
            <input ref={ref} />
        </label>
    );
});
```

## Zastosowanie

-   ze względu na komplikowanie kodu, raczej wyłącznie do prostych, niskolevelowych komponentów typu buttony, inputy
- nie nadużywać, raczej wyłącznie do rzeczy, które nie mogą być użyte jako propsy, np. focus, scroll, select text itp.

## <a href='./useImperativeHandle.md'>useImperativeHandle()</a>

-   aby ograniczyć ekspozycję nodea, można wystawić tylko wybrany obiekt operujący na tym nodzie, poprzez użycie `useImperativeHandle()`.

```js
import { forwardRef, useRef, useImperativeHandle } from 'react';

const MyInput = forwardRef(function MyInput(props, ref) {
    const inputRef = useRef(null);

    // powiąż ref z rodzica i inputRef
    useImperativeHandle(
        ref,
        () => {
            return {
                // przypisz metody do inputRef
                focus() {
                    inputRef.current.focus();
                },
            };
        },
        []
    );

    return <input {...props} ref={inputRef} />;
});

export default MyInput;
```

<br/>
<br/>
<br/>

<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>
<a href='#top' style='border: 1px solid gold; padding: 5px; color: gold'>↑ back to top</a>
