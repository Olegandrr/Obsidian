![Что такое React хуки (Hooks)?](https://youtu.be/RpcB5jnJvcI?t=475)

#### Ответ

Подробнее: [[0044 Все хуки и концепты React]]

![[Pasted image 20230704185145.png|600]]

*React хуки (Hooks)* - это новый механизм, появившийся в React 16.8, который позволяет использовать состояние и другие возможности React в функциональных компонентах.

В React встроены некоторые хуки, такие как `useState()`, `useEffect()`, `useContext()`, `useReducer()` и другие. Вы также можете создавать собственные хуки для повторного использования логики между компонентами.

##### useState()

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

*useState() всегда обновляет обьект полностью, а не отдельные поля, как setState().* При этом, useState() может принимать в себе, в качестве начального значения, состояния state, так и в результате, функцию-обработчик.

##### useEffect()

*Хук `useEffect()`* используется для добавления эффектов в функциональный компонент:

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

Напоминание: не обновляйте состояние внутри useEffect без продуманной логики, иначе это может вызвать бесконечный круг перерисовок.

*Скобки, `[]`, представляющие пустой массив, означают, что эффект не использует значения, участвующие в потоке данных React, и по этой причине безопасным можно считать его однократное применение.* Кроме того, использование пустого массива зависимостей является обычным источником ошибок в том случае, если некое значение, на самом деле, используется в эффекте. 

Вам понадобится освоить несколько стратегий (преимущественно, представленных в виде `useReducer` и `useCallback`), которые могут помочь устранить необходимость в зависимости вместо того, чтобы необоснованно эту зависимость отбрасывать.

###### Функция очистки

Внутри useEffect всегда можно вернуть функцию очистки, которая используется для удаления нежелательного поведения. Функция очистки вызывается не только перед размонтированием компонента, но и перед выполнением следующего эффекта.

```jsx
useEffect(() => {
	console.log(`state1 changed | ${state1}`);
	return () => {
		console.log('state1 unmounted | ', state1);
	}
}, [state1])
```

###### useEffect() на практике

~~~ jsx
useEffect (() => {
	console.log(a + b + c);
	return () => console.log('cleanup')
}, [a , b, c]);
~~~

Если вернуть функцию , она будет вызываться для очистки предыдущего эффекта (похоже на #componentWillUnmount())

~~~ jsx
useEffect(() => console.log('mount') , [] );
useEffect(() => console.log('update'));
useEffect(() => () => console.log('unmount'), []);
~~~

// effect + cleanup ( mount + unmount )

~~~ jsx
useEffect(() => {
	const timeout = setTimeout(setVisible, 10, false);
	return () => clearTimeout(timeout);
}, []);
~~~

Если данные зависят от параметра (например, ID ресурса) - обязательно укажите его в массиве > Promise нельзя отменить, но можно проигнорировать результат:

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

##### useContext()

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

##### useReducer()

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

*useReducer более предпочтителен нежели useState когда у вас сложная логика, которая включает в себя несколько значений, или когда обновляемое состояние зависит от предыдущего. useReducer также позволяет оптимизировать компонент, так как вы можете передавать dispatch из вне вместо коллбэка.*

____
#React #Hooks #useState #useEffect #useReducer #useContext 

____

#### [[004 React + Redux|Назад]]