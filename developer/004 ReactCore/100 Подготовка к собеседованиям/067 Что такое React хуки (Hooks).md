![Что такое React хуки (Hooks)?](https://youtu.be/RpcB5jnJvcI?t=475)

![](https://www.youtube.com/watch?v=3Ku62Nh1mhk)
#### Ответ

Подробнее: [[0044 Все хуки и концепты React]] , [Вопросы для собеседования по хукам React](https://habr.com/ru/articles/534632/), [Обработка ошибок в React Hooks](https://nuancesprog.ru/p/9823/)

![[Pasted image 20230704185145.png|600]]

*React Hooks* - это новый механизм, появившийся в React 16.8 (2019 год), который позволяет использовать состояние и другие возможности React в функциональных компонентах. 

В React встроены некоторые хуки, такие как `useState()`, `useEffect()`, `useContext()`, `useReducer()` и другие. Вы также можете создавать собственные хуки для повторного использования логики между компонентами.

*Хуки чувствительны к порядку выполнения:*
1. Устанавливаем *Dispatcher*;
2. Инициализируется *очередь хуков*, сбрасываем *количество рендеров*;
3. Запускаем *функцию компонента*;
4. После каждого встреченного хука *меняем указатель* в списке хуков на +1 ;
5. После рендера смот рим, были ли *изменения стейта*? (useState/useReducer dispatch) - *если да*, то переходим на *п.3* увеличивая *счётчик рендеров*;
25 вызовов компонентов максимально.

Последовательность хуков, формируемая React при первом рендеринге, выглядит следующим образом (представим, что прямоугольники — это хуки, каждый хук содержит указатель на следующий):
![[Pasted image 20230916132451.png|600]]

*Изменили состояние компонента, обновился родительский компонент или же изменился пропс - весь код в теле выполняется при каждом обновлении.*

«React следит за тем, какой компонент рендерится в данный момент.… Существует **внутренний список ячеек памяти, связанных с каждым компонентом**. Они являются JavaScript-объектами, в которых мы можем хранить **некоторые данные**. Когда вызывается некий хук, например useState(), он **читает значение текущей ячейки (или инициализирует её во время первого рендера) и двигает указатель на следующую**. Таким способом каждый вызов useState() получит своё независимое состояние.»

1. React узнаёт экземпляр компонента, в котором был вызван `useState` ;
2. `useState` делегирует в `updateReducer` действия в случае обновления (повторного рендеринга)
3. fiber-волокно будет указывать на экземпляр компонента, который вызывался `useState`, React ставит в очередь повторного рендеринга этого компонента , когда присваивается новое значение состояния;

Подробнее: [Заметка о том, как работают хуки](https://habr.com/ru/articles/553104/)
##### Немного об `ограничениях...`

«...Не вызывайте хуки внутри циклов, условных операторов или вложенных функций. Вместо этого всегда используйте хуки только внутри React-функций, до возврата какого-либо значения из них. Исполнение этого правила гарантирует, что хуки вызываются **в одинаковой последовательности при каждом рендере компонента**. Это позволит React правильно сохранять состояние хуков между множественными вызовами `useState()` и `useEffect()`»

##### `useState()`

*Хук `useState()`* используется для добавления состояния в функциональный компонент:

``` JSX
import React, { useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default MyComponent;
```

В данном примере мы используем хук `useState()` для добавления состояния `count` в функциональный компонент `MyComponent`. 
*Хук `useState()` возвращает массив, в котором первый элемент - текущее значение состояния, а второй элемент - функция для обновления состояния.* В данном случае мы используем деструктуризацию массива, чтобы извлечь текущее значение состояния и функцию для обновления состояния.

*`useState()` всегда обновляет объект полностью, а не отдельные поля, как `setState()`* При этом, useState() может принимать в себе, в качестве начального значения, состояния state, так и в результате, функцию-обработчик. 

###### Передача в качестве начального состояния функции-инициализатора

Этот пример передает функцию инициализатора, поэтому функция `createInitialTodos` выполняется только во время инициализации. Она не выполняется при повторном рендеринге компонента, например, когда вы вводите текст в поле ввода.

```jsx
import { useState } from 'react';

function createInitialTodos() {
    const initialTodos = [];
    for (let i = 0; i < 50; i++) {
        initialTodos.push({
            id: i,
            text: 'Item ' + (i + 1),
        });
    }
    return initialTodos;
}

export default function TodoList() {
    const [todos, setTodos] = useState(createInitialTodos);
    const [text, setText] = useState('');

    return (
        <>
            <input
                value={text}
                onChange={(e) => setText(e.target.value)}
            />
            <button
                onClick={() => {
                    setText('');
                    setTodos([
                        {
                            id: todos.length,
                            text: text,
                        },
                        ...todos,
                    ]);
                }}
            >
                Add
            </button>
            <ul>
                {todos.map((item) => (
                    <li key={item.id}>{item.text}</li>
                ))}
            </ul>
        </>
    );
}
```
###### batching

*`setState` - асинхронная функция. Под капотом React объединяет все мутации состояний, благодаря чему код функционального компонента будет вызван 1 раз, это называется* **"batching"**. #batching

Подробнее: [Batching](https://dev.to/shivamjjha/batching-in-react-4pp3)

```jsx
import React, { useState, FC } from "react";

export const ExampleFuncComponent: FC = () => {
  const [count, setCount] = useState(0);
  
  const onClick0 = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
  };
  
  const onClick1 = () => {
    setCount((v) => v + 1);
    setCount((v) => v + 1);
    setCount((v) => v + 1);
  };
  
  return (
    <div>
      <div>{count.toString()}</div>
      <button onClick={onClick0}>
	      test 0
      </button>
      <button onClick={onClick1}>
  	    test 1
      </button>	
    </div>
  );
};
```

При нажатии на `test 1` счетчик увеличится на 3, а при нажатии на `test 0` только на 1. Почему это происходит:

```jsx
// Например count = 0
const onClick0 = () => {
  // count + 1 = 0 + 1;
  setCount(count + 1);
  // Здесь можем ожидать, что count уже 1, но т.к. вызов setState асинхронный
  // состояние еще не изменено, поэтому count по-прежнему 0
  // count + 1 = 0 + 1;
  setCount(count + 1);
  // count + 1 = 0 + 1;
  setCount(count + 1);
};
```

Поэтому если новое состояние опирается на предыдущее состояние, используйте функцию:

```jsx
const onClick1 = () => {
  setCount(v => v + 1);
  setCount(v => v + 1);
  setCount(v => v + 1);
};
```

**Ещё немного про `batching`**

```jsx
function ExampleComponent() { 
	const [count, setCount] = useState(0); 
	const handleClick = () => { 
	// Несколько вызовов `setCount` будут сгруппированы в один батч 
	setCount(count + 1); 
	setCount(count + 2); 
	setCount(count + 3); 
};
```

![](https://www.youtube.com/watch?v=bE4mXoNlovM)

##### `useEffect()`

Подробно: [Полное руководство по useEffect()](https://habr.com/ru/companies/ruvds/articles/445276/)

_Эффекты_ позволяют выполнить некоторый код после рендеринга.

*Хук `useEffect()`* используется для добавления эффектов в функциональный компонент, работают за счёт `fiber.node`:

``` JSX
import React, { useState, useEffect } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default MyComponent;
```

В данном примере мы используем хук `useEffect()` для добавления эффекта обновления заголовка документа при изменении состояния `count`. *Хук `useEffect()` принимает функцию, которая будет выполнена после каждого рендеринга компонента.* В данном случае мы обновляем заголовок документа с помощью свойства `document.title`.

###### Что такое массив зависимостей [] ?

**Массив** **зависимостей** - это список переменных состояния или функций, от которых **зависит** хук **useEffect**. При изменении этих значений срабатывает функция обратного вызова **useEffect**. Используя **массив** **зависимостей**, мы можем предотвратить чрезмерный повторный рендеринг компонентов, что делает код более эффективным.

```jsx
const [state1, setState1] = useState(0);
const [state2, setState2] = useState(0);
useEffect(() => {
	console.log('state1 changed');
}, [state1])
```

*Напоминание: не обновляйте состояние внутри `useEffect()` без продуманной логики, иначе это может вызвать бесконечный круг перерисовок.*

*Скобки, `[]`, представляющие пустой массив, означают, что эффект не использует значения, участвующие в потоке данных React, и по этой причине безопасным можно считать его однократное применение.* Кроме того, использование пустого массива зависимостей является обычным источником ошибок в том случае, если некое значение, на самом деле, используется в эффекте. 

Вам понадобится освоить несколько стратегий (преимущественно, представленных в виде `useReducer` и `useCallback`), которые могут помочь устранить необходимость в зависимости вместо того, чтобы необоснованно эту зависимость отбрасывать.

###### Функция очистки

*Внутри useEffect всегда можно вернуть функцию очистки, которая используется для удаления нежелательного поведения.* Функция очистки вызывается не только перед размонтированием компонента, но и перед выполнением следующего эффекта.

```jsx
useEffect(() => {
    // Выполняем какие-то действия при монтировании компонента
	console.log(`state1 changed | ${state1}`);
	// Возвращаем функцию очистки
	return () => {
		console.log('state1 unmounted | ', state1);
		// Выполняем очистку ресурсов или отмену подписок
	}
}, [state1])
```


###### Как ведет себя замыкание в хуках

При обновлении компонента все переменные в нем создаются по-новой. При этом, в памяти хранится предыдущий effect (которую передавали в useEffect). *Предыдущий effect завязан на предыдущее окружение, она через замыкания имеет доступ ко всем переменным, внутри компонента и значение этих переменных соответствует предыдущему состоянию компонента.* Таким образом в памяти хранится два экземпляра всех переменных и функция, которую мы создаем в useMemo, useCallback, useEffect и прочих, на самом деле не теряет замыкания, это мы "теряем" текущую функцию.

###### `useEffect()` на практике

1. Если вернуть функцию , она будет вызываться для очистки предыдущего эффекта (похоже на #componentWillUnmount())

~~~ jsx
useEffect (() => {
	console.log(a + b + c);
	return () => console.log('cleanup')
}, [a , b, c]);
~~~

2. effect + cleanup ( mount + unmount )
	`2.1`
~~~ jsx
useEffect(() => console.log('mount') , [] );
useEffect(() => console.log('update'));
useEffect(() => () => console.log('unmount'), []);
~~~
	2.2
~~~ jsx
useEffect(() => {
	const timeout = setTimeout(setVisible, 10, false);
	return () => clearTimeout(timeout);
}, []);
~~~

3. Если данные зависят от параметра (например, ID ресурса) - обязательно укажите его в массиве > Promise нельзя отменить, но можно проигнорировать результат:

~~~ jsx
useEffect(() => {
	let cancelled = false;
	fetch(`/users/${id}`)
		.then(res => res.json())
		.then(data => !cancelled && setName(data.name));
	return () => cancelled = true; }, [id]
);
~~~

###### Как осуществлять обработку данных из списка?

Подробнее: [DATA FETCHING WITH REACT HOOKS](https://www.robinwieruch.de/react-hooks-fetch-data/)

###### Как пропустить `useEffect()` при первом рендеринге

Мы можем использовать `useRef()` для сохранения любого изменяемого значения, которое мы хотим, чтобы отслеживать, выполняется ли `useEffect()` впервые.

Если мы хотим, чтобы эффект выполнялся на той же фазе, что и `componentDidUpdate()` выполняется, мы можем использовать [`useLayoutEffect()`](https://reactjs.org/docs/hooks-reference.html#uselayouteffect) вместо этого.

```jsx
const { useState, useRef, useLayoutEffect } = React;

function ComponentDidUpdateFunction() {
  const [count, setCount] = useState(0);

  const firstUpdate = useRef(true);
  useLayoutEffect(() => {
    if (firstUpdate.current) {
      firstUpdate.current = false;
      return;
    }

    console.log("componentDidUpdateFunction");
  });

  return (
    <div>
      <p>componentDidUpdateFunction: {count} times</p>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        Click Me
      </button>
    </div>
  );
}

ReactDOM.render(
  <ComponentDidUpdateFunction />,
  document.getElementById("app")
);
```

######  `AbortController`

[AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController) - это специальный объект, который содержит свойство **signal**. Это свойство можно добавить к асинхронной функции, используя fetch в качестве одной из [опций](https://developer.mozilla.org/en-US/docs/Web/API/fetch). Это связывает определенный сигнал с определенной функцией. Но зачем это делать?

Еще одним методом AbortController является **abort()**, который способен **отменить выполнение функции**. Это означает, что если сервер отвечает, браузер проигнорирует этот ответ, и он **не будет передавать колбэк в наш стек вызовов**. Хорошо, но как это можно использовать?

С тех пор как были введены **хуки**, мы можем получить доступ к жизненному циклу функциональных компонентов, используя [useEffect](https://reactjs.org/docs/hooks-reference.html#useeffect). В отношении того, как он используется, он может вести себя как детектор событий **монтирования, размонтирования или обновления** компонента. Вот несколько основных примеров:

```jsx
const [showLoading, setShowLoading] = useState(false)

 useEffect(
    () => {
      let timer1 = setTimeout(() => setShowLoading(true), 1000)

      // здесь происходит очищение таймаута при размонтировании компонента
      // как при componentWillUnmount
      return () => {
        clearTimeout(timer1)
      }
    },
    [] //useEffect сработает один раз
       //если передадим значение в массив, наример так [data], тогда 
       //clearTimeout будет срабатывать каждый раз когда значение date меняется
  )
```

**Отмена асинхронного сигнала для событий, вызванных монтированием компонента**

Итак, после того, как мы рассмотрели базовую теорию, давайте посмотрим случай, когда нам нужно **получить** некоторые **данные из API сразу после монтирования компонента**:

```jsx
export const Articles = () => {
  const [state, setState] = useState([]);

  useEffect(() => {
    const abortController = new AbortController();
    const {signal} = abortController;

    const apiCall = async path => {
      try {
        const request = await fetch(path, {
          signal: signal,
          method: 'GET',
        });
        const response = await request.json();
        setState([response]);
      } catch (e) {
        if (!signal?.aborted) {
          console.error(e);
        }
      }
    };

    apiCall('https://jsonplaceholder.typicode.com/posts/1');

    return () => {
      abortController.abort();
    };
  }, [setState]);

  return (
    <>
      {state.map(article=> (
        <article key={article?.id} className='article'>
          <h1>{article?.title}</h1>
          <p>{article?.body}</p>
        </article> 
      ))}
    </>
  );
};
```

На первый взгляд это кажется немного сложным, но на самом деле это, вероятно, один из самых простых примеров использования AbortController :) Просто перед размонтированием компонента я вызываю метод AbortController.abort(). Вот и все!

Подробнее: [React, AbortController и асинхронные onClick вызовы](https://habr.com/ru/articles/588799/)
##### `useContext()`

*Хук `useContext()`* используется для получения значения контекста в функциональном компоненте:

```JSX
import React, { useContext } from 'react';
import MyContext from './MyContext';

function MyComponent() {
  const value = useContext(MyContext);

  return <div>{value}</div>;
}

export default MyComponent;
```

В данном примере мы используем хук `useContext()` для получения значения контекста `MyContext` в функциональном компоненте `MyComponent`. Хук `useContext()` возвращает текущее значение контекста.

**Отличия между useContext() и Redux**

| useContext()                                                                                                       | Redux                                                                   |
| ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| useContext() - это хук                                                                                             | Redux - это библиотека управления состоянием.                           |
| Он используется для обмена данными.                                                                                | *Он используется для управления данными и состоянием.*                    |
| Изменения вносятся с учетом значения контекста.                                                                    | Изменения вносятся с помощью чистых функций, т.е. редукторов.           |
| Мы можем изменить состояние в нем.                                                                                 | *Состояние доступно только для чтения.* Мы не можем изменить их напрямую. |
| Он повторно рендерит все компоненты всякий раз, когда происходит какое-либо обновление в prop значения поставщика. | Производит только повторный рендеринг обновленных компонентов.                 |
| Его лучше использовать с небольшими приложениями.                                                                  | Идеально подходит для более крупных применений.                      |
| Хук легче для понимания и требует меньше кода.                                                                     | Redux довольно сложен для понимания.                                      |

##### `useReducer()`

*`useReducer()` более предпочтителен нежели `useState()` когда у вас сложная логика, которая включает в себя несколько значений, или когда обновляемое состояние зависит от предыдущего. `useReducer()` также позволяет оптимизировать компонент, так как вы можете передавать `dispatch()` из вне вместо коллбэка.*

*Хук `useReducer()`* используется для управления состоянием с помощью редуктора в функциональном компоненте:

```JSX
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function MyComponent() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>You clicked {state.count} times</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </div>
  );
}

export default MyComponent;
```

В данном примере мы используем хук `useReducer()` для управлением состояния `count` с помощью редуктора `reducer` в функциональном компоненте `MyComponent`. *Хук `useReducer()` возвращает текущее состояние и функцию для диспетчеризации действий. Мы передаем вторым аргументом начальное состояние объекта `{ count: 0 }` и редуктор `reducer`, который обрабатывает действия `increment` и `decrement`.* В методе `render()` мы используем функцию диспетчеризации `dispatch()` для вызова соответствующих действий при нажатии на кнопки.

____
#React #Hooks #useState #useEffect #useReducer #useContext #AbortController

____

#### [[004 React + Redux|Назад]]