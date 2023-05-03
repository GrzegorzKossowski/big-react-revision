<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a>

# useCallback

`useCallback(fn, [dependencies])`

Przetrzymuje funkcję między renderowaniami komponentu.

-   tworzy nową funkcję, ale jeśli dependencje się nie zmieniły, zwraca starą wersję.
-   brak tablicy dependency powoduje wykonanie za każdym razem
-   w zależnościach można podawać propsy, zmienne, funkcje

## Zastosowanie

1. przekazywanie funkcji do komponentu dziecka opakowanego w funkcję `memo` (która ogranicza rerendering komponentu)

```js
export const ProductPage = ({ productId }) => {
    // useCallback na funkcji
    const handleSubmit = useCallback(
        orderDetails => {
            //...
        },
        [productId]
    );

    return (
        //...
        <ShippingForm onSubmit={handleSubmit} />
    );
};
// komponent dziecka opakowany w memo
const ShippingForm = memo(function ShippingForm({ onSubmit }) {
    //...
});
```

2. przekazanie funkcji do innego hooka, który od niej zależy. Jeśli funkcja nie zmieniła się, hook (np. useEffect) się nie wykona. [docs](https://react.dev/reference/react/useCallback#preventing-an-effect-from-firing-too-often)

-   optymalizacja: jeśi to możliwe, wstawienie funkcji do docelowego hooka (np. useEffect)

3. opakowanie funkcji zwracanych z własnych hooków w useCallback (aby nie były tworzone ciągle na nowo) [docs](https://react.dev/reference/react/useCallback#optimizing-a-custom-hook)

```js
function foo() {
    const { dispatch } = useContext(RouterStateContext);

    // ✅ zapisać funkcję w useCallback(), by nie tworzyła się ciągle na nowo
    const navigate = useCallback(
        url => {
            dispatch({ type: 'navigate', url });
        },
        [dispatch]
    );
    // ✅ zapisać funkcję w useCallback(), by nie tworzyła się ciągle na nowo
    const goBack = useCallback(() => {
        dispatch({ type: 'back' });
    }, [dispatch]);

    return {
        navigate,
        goBack,
    };
}
```

## Ograniczenia

-   jako hook może być użyty tylko w głównym zakresie komponentu lub w innym hooku

## ⚠️ Update stanu wewnątrz hooka

-   jeśli zmiana stanu następuje wewnątrz hooka, **na podstawie starego stanu**, nie używać go w tablicy zależności

```js
const [todos, setTodos] = useState([]);

const handleAddTodo = useCallback(
    text => {
        const newTodo = { id: nextId++, text };
        setTodos([...todos, newTodo]); // 🛑 NIE!
    },
    [todos]
);
```

```js
const [todos, setTodos] = useState([]);

const handleAddTodo = useCallback(text => {
    const newTodo = { id: nextId++, text };
    setTodos(todos => [...todos, newTodo]);
}, []); // ✅ No need for the todos dependency
```

<br/>
<br/>
<br/>

<a href='../../README.md' id='top' style='border: 1px solid gold; padding: 5px; color: gold'>← back to README.md</a> <a href='#top' style='border: 1px solid gold; padding: 5px; color: gold'>↑ back to top</a>
