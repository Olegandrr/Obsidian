![Что такое React хуки (Hooks)?](https://youtu.be/RpcB5jnJvcI?t=475)

#### Ответ

![[Pasted image 20230704185145.png|600]]

*React хуки (Hooks)* - это новый механизм, появившийся в React 16.8, который позволяет использовать состояние и другие возможности React в функциональных компонентах. Хуки позволяют использовать состояние и другие возможности React без необходимости создания классовых компонентов. Хуки также упрощают повторное использование логики между компонентами.

В React встроены некоторые хуки, такие как `useState()`, `useEffect()`, `useContext()`, `useReducer()` и другие. Вы также можете создавать собственные хуки для повторного использования логики между компонентами.

##### useState()

*Хук `useState()`* используется для добавления состояния в функциональный компонент:

```JSX
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

В данном примере мы используем хук `useState()` для добавления состояния `count` в функциональный компонент `MyComponent`. Хук `useState()` возвращает массив, в котором первый элемент - текущее значение состояния, а второй элемент - функция для обновления состояния. В данном случае мы используем деструктуризацию массива, чтобы извлечь текущее значение состояния и функцию для обновления состояния.

##### useEffect()

*Хук `useEffect()`* используется для добавления эффектов в функциональный компонент:

```JSX
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

В данном примере мы используем хук `useEffect()` для добавления эффекта обновления заголовка документа при изменении состояния `count`. Хук `useEffect()` принимает функцию, которая будет выполнена после каждого рендеринга компонента. В данном случае мы обновляем заголовок документа с помощью свойства `document.title`.

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

В данном примере мы используем хук `useReducer()` для управлением состояния `count` с помощью редуктора `reducer` в функциональном компоненте `MyComponent`. Хук `useReducer()` возвращает текущее состояние и функцию для диспетчеризации действий. Мы передаем вторым аргументом начальное состояние объекта `{ count: 0 }` и редуктор `reducer`, который обрабатывает действия `increment` и `decrement`. В методе `render()` мы используем функцию диспетчеризации `dispatch()` для вызова соответствующих действий при нажатии на кнопки.

Подробнее: [[Все хуки и концепты React]]

____
#React #Hooks #useState #useEffect #useReducer #useContext 

____

#### [[004 React + Redux|Назад]]