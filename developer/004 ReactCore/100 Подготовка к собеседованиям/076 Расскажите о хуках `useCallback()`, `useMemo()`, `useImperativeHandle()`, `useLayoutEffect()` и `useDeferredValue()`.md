![Расскажите о хуках `useCallback()`, `useMemo()`, `useImperativeHandle()`, `useLayoutEffect()`?](https://youtu.be/GZUy2i6QN7o?t=449)

#### Ответ

![[Pasted image 20230704190031.png|600]]

Хуки `useCallback()`, `useMemo()`, `useImperativeHandle()`, и `useLayoutEffect()` - это дополнительные хуки в React, которые позволяют оптимизировать производительность и управлять поведением компонентов.

##### *`useCallback()`:*

 *`useCallback()` возвращает мемоизированную версию функции, которая не будет пересоздаваться при каждом рендеринге компонента, если ее зависимости не изменились.*
 
*`useCallback()` под капотом тот же `useMemo()` и по сути является синтаксическим сахаром.*

```jsx
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

В этом примере, `memoizedCallback` - это мемоизированная версия функции `doSomething`, которая будет пересоздаваться только тогда, когда изменятся зависимости `a` или `b`.

*`useCallback()` не работает с классическими замыканиями, но прекрасно работает с замыканиями, созданными с помощью `useRef()`*

Таким образом, одно из основных применений `useCallback()` - это оптимизация производительности рендеринга, путём кеширования функций, которые вы передаете дочерним компонентам.

Если вы пишете кастомный хук, рекомендуется обернуть все функции, которые он возвращает, в `useCallback()`

```jsx
function useRouter() {  

	const { dispatch } = useContext(RouterStateContext);  

	const navigate = useCallback((url) => {  
		dispatch({ type: 'navigate', url });  
	}, [dispatch]);  

	const goBack = useCallback(() => {  
		dispatch({ type: 'back' });  
	}, [dispatch]);  

	return {  
		navigate,  
		goBack,  
	};  
}
```

Иногда вы можете захотеть вызвать функцию внутри [Effect:](https://reactdev.ru/learn/synchronizing-with-effects/) 

```jsx
function ChatRoom({ roomId }) {
    const [message, setMessage] = useState('');

    function createOptions() {
        return {
            serverUrl: 'https://localhost:1234',
            roomId: roomId,
        };
    }

    useEffect(() => {
        const options = createOptions();
        const connection = createConnection();
        connection.connect();
        // ...
    });
}
```

Это создает проблему. [Каждое реактивное значение должно быть объявлено зависимостью вашего Эффекта](https://reactdev.ru/learn/lifecycle-of-reactive-effects/) Однако, если вы объявите `createOptions` как зависимость, это заставит ваш Эффект постоянно переподключаться к чату:

```jsx 
useEffect(() => {
    const options = createOptions();
    const connection = createConnection();
    connection.connect();
    return () => connection.disconnect();
}, [createOptions]); // 🔴 Problem: This dependency changes on every render
// ...
```

Чтобы решить эту проблему, вы можете обернуть функцию, которую нужно вызвать из Effect, в `useCallback`:

```jsx
function ChatRoom({ roomId }) {
    const [message, setMessage] = useState('');

    const createOptions = useCallback(() => {
        return {
            serverUrl: 'https://localhost:1234',
            roomId: roomId,
        };
    }, [roomId]); // ✅ Only changes when roomId changes

    useEffect(() => {
        const options = createOptions();
        const connection = createConnection();
        connection.connect();
        return () => connection.disconnect();
    }, [createOptions]); // ✅ Only changes when createOptions changes
    // ...
}
```

Это гарантирует, что функция `createOptions` будет одинаковой между повторными рендерингами, если `roomId` одинаков. **Однако, еще лучше устранить необходимость в зависимости от функции.** Переместите вашу функцию _внутрь_ Effect:

```jsx
function ChatRoom({ roomId }) {
    const [message, setMessage] = useState('');

    useEffect(() => {
        function createOptions() {
            // ✅ No need for useCallback or function dependencies!
            return {
                serverUrl: 'https://localhost:1234',
                roomId: roomId,
            };
        }

        const options = createOptions();
        const connection = createConnection();
        connection.connect();
        return () => connection.disconnect();
    }, [roomId]); // ✅ Only changes when roomId changes
    // ...
}
```

Теперь ваш код стал проще и не нуждается в `useCallback`. [Подробнее об удалении зависимостей от эффектов.](https://reactdev.ru/learn/removing-effect-dependencies/)

Подробнее: [useCallback()](https://reactdev.ru/reference/useCallback/#usecallbackfn-dependencies)

##### *`useMemo()`:*
 
**useMemo()** - это хук, который сохраняет результат вызова функции (первый аргумент) и пересчитывает его только при изменении зависимостей (второй аргумент). `useMemo()` возвращает результат вызова первого аргумента.

``` jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

Хук `useMemo()` также используется для оптимизации производительности.

В этом примере, `memoizedValue` - это мемоизированное значение, которое будет пересоздаваться только тогда, когда изменятся зависимости `a` или `b`.

Вызов useMemo имеет свою цену и это нужно понимать. Хорошо про цену рассказано [тут](https://youtu.be/i6DPqqbdIyw). Для себя я вывел следующее правило:

*Если сложность вычислений больше O(n), я использую useMemo. Если сложность вычислений постоянная или O(log n) - не использую. Про сложность хорошо рассказано [тут](https://tproger.ru/articles/computational-complexity-explained/).*

**useMemo()** стоит использовать в двух случаях:
1. Когда в компоненте выполняются сложные вычисления useMemo сохранит их и лишняя работа будет упразднена.
2. Когда нужно передать ссылочный тип данных в **мемоизированный** компонент.*

##### Отличия useCallback() и useMemo()

Подробно: [Разница между useMemo и useCallback подробно](https://habr.com/ru/articles/579242/)

| useCallback()                                                                                                                                      | useMemo()                                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| *возвращает мемоизированную версию функции, которая будет пересоздаваться при каждом рендеринге компонента, если ее зависимости изменились.* | *возвращает мемоизированное значение, которое будет пересоздаваться при каждом рендеринге компонента, если ее зависимости изменились.*                                             |
| *вызывается пользователем*                                                                                                                         | *вызывается исходниками React*                                                                                                                                 |
| ---------                                                                                                                                        | *внутри не используются другие хуки, т.к. useMemo() отрабатывает на стадии рендеринга, модификация состояния запустит процесс заново. Произойдет зацикливание* |
| *использует переданные аргументы*                                                                                                                  | *игнорирует переданные аргументы*                                                                                                                              |
| *обязателен массив зависимостей, в случае отсутствия будет постоянный ререндер*                                                                    | *разрешен undefined, но нельзя делать его опциональным*                                                                                                                                                             |

`useCallback()` - сохраняет функцию между вызовами, если данные в массиве зависимостей не изменились. `useMemo()` - работает также, но для значений.

##### *`useLayoutEffect()`:*

Хук `useLayoutEffect()` выполняет те же действия, что и `useEffect()`, но вызывает эффект синхронно после всех изменений в DOM. *Он может использоваться для выполнения действий, которые зависят от размеров или позиций элементов в DOM.*

```jsx
useLayoutEffect(() => {
  // выполнить действия после изменений в DOM
}, [deps]);
```

В этом примере, `useLayoutEffect()` вызывает функцию после изменений в DOM, когда зависимости изменились. Он может быть полезен для выполнения действий, которые зависят от размеров или позиций элементов в DOM, например, для выполнения анимации.

| useLayoutEffect()                                             | useEffect()                                                                                                                                                                                                                   |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| синхронное выполнение хука                                    | асинхронное выполнение хука                                                                                                                                                                                                   |
| будет вызван **после** того, как браузер отрисует компоненты.     | будет вызван **до** того, как браузер сможет отрисовать компоненты. Срабатывает когда компоненты уже находятся на Virtual DOM (в памяти и можно прочитать/установить различные свойств), но еще не были отрисованы браузером. |
| применяет сайдэфекты ПОСЛЕ фазы отрисовки (paint) в браузере. | применяет сайдэфекты после расчёта макета (dom calculating / layout / reflow) страницы и ДО фазы отрисовки (paint) в браузере.                                                                                                |

##### *`useImperativeHandle()`:*

Хук `useImperativeHandle()` используется для управления экземпляром компонента, который может быть доступен из родительского компонента. *Он позволяет определить функции, которые должны быть доступны родительскому компоненту.*

```jsx
useImperativeHandle(ref, () => ({
  focus: () => {
    inputRef.current.focus();
  }
}));
```

В этом примере, `useImperativeHandle()` позволяет определить функцию `focus()`, которая будет доступна родительскому компоненту через `ref`.

##### `useDeferredValue()`

`useDeferredValue()` - это хук, который позволяет отложить обновление части пользовательского интерфейса.

```jsx
const deferredValue = useDeferredValue(value);
```

Вызовите `useDeferredValue()` на верхнем уровне вашего компонента, чтобы получить отложенную версию этого значения. `value`: Значение, которое вы хотите отложить. Оно может иметь любой тип.

____
#React #Hooks #useCallback #useMemo #useImperativeHandle #useLayoutEffect #useDeferredValue

____

#### [[004 React + Redux|Назад]]