![Что такое `useReducer()`?](https://youtu.be/GZUy2i6QN7o?t=257)

#### Ответ

![[Pasted image 20230704185920.png|600]]

*`useReducer()`* - это хук в React, который позволяет управлять состоянием компонента с помощью редуктора (reducer) в стиле Redux.

*Редуктор (reducer) - это функция, которая принимает текущее состояние и действие (action), и возвращает новое состояние.* В React, редуктор может использоваться для управления сложным состоянием компонента, которое может включать в себя несколько свойств.

Хук `useReducer()` имеет синтаксис следующего вида:

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

Здесь:
- `state` - текущее состояние компонента
- `dispatch` - функция, которая позволяет отправлять действия (action) в редуктор для обновления состояния
- `reducer` - функция-редуктор, которая принимает текущее состояние и действие, и возвращает новое состояние
- `initialState` - начальное состояние компонента

Когда компонент рендерится в первый раз, `useReducer()` вызывает редуктор с начальным состоянием и возвращает текущее состояние и функцию `dispatch`. Когда функция `dispatch` вызывается с действием (action), `useReducer()` вызывает редуктор с текущим состоянием и действием, и возвращает новое состояние.

Вот пример кода, который демонстрирует, как использовать `useReducer()` для управления состоянием компонента:

```jsx
import { useReducer } from 'react';

function MyComponent() {
  const initialState = { count: 0 };
  
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

  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h1>Количество: {state.count}</h1>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </div>
  );
}
```

В этом примере, `useReducer()` используется для управления состоянием компонента `MyComponent`, который включает в себя счетчик. Редуктор `reducer` определяет два действия: увеличение и уменьшение счетчика. Хук `useReducer()` используется для создания текущего состояния и функции `dispatch`, которая позволяет отправлять действия в редуктор для обновления состояния. Кнопки `+` и `-` используют функцию `dispatch` для отправки действий в редуктор и обновления состояния.

____
#React #useReducer #Hooks 

____

#### [[004 React + Redux|Назад]]