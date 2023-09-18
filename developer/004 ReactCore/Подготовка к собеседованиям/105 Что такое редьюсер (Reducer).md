![Что такое редьюсер (Reducer)?](https://youtu.be/HBSAjY-xh3k?t=573)

![](https://www.youtube.com/watch?v=HwSqZsN0qc0)

#### Ответ

![[Pasted image 20230704193008.png|600]]

*Редюсер (`reducer`) — это чистая функция, которая принимает предыдущее состояние и экшен (`state` и `action`) и возвращает следующее состояние (новую версию предыдущего).*

``` jsx
(previousState, action) => newState
```

*Если previousState - underfined , то нужно вернуть первоначальный (initial) state .*

*Редьюсеры должны быть чистыми функциями, то есть они не должны изменять состояние напрямую, а только возвращать новый объект состояния. Это обеспечивает предсказуемость и консистентность в приложении и упрощает отладку и тестирование.*

Функция называется редюсером (reducer) потому, что ее можно передать в [`Array.prototype.reduce(reducer, ?initialValue)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce). 

В `reducer` никогда нельзя:
-   Непосредственно изменять то, что пришло в аргументах функции;
-   Выполнять какие-либо сайд-эффекты: обращаться к API или осуществлять переход по роутам;
-   Вызывать не чистые функции, например `Date.now()` или `Math.random()`.

Вот пример простого редьюсера, который обрабатывает действие INCREMENT и увеличивает счетчик на 1:

```jsx
function counterReducer(state = { count: 0 }, action) {
  switch (action.type) {
    case 'INCREMENT':
      return { ...state, count: state.count + 1 };
    default:
      return state;
  }
}
```

*`Reducer` является ключевым элементом в управлении состоянием приложения и позволяет обрабатывать действия, которые изменяют состояние приложения. Он может быть объединен с другими reducer'ами с помощью функции `combineReducers` для управления состоянием всего приложения в единый редьюсер (root reducer).*

*Когда вы разбиваете базовый reducer на несколько, то название каждого из них должно соответствовать полю которое он обновляет в `store`.*

Подробнее: [Reducers](https://rajdee.gitbooks.io/redux-in-russian/content/docs/basics/Reducers.html)

____
#React #redux #reducer

____

### [[004 React + Redux|Назад]]