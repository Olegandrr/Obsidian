![Что такое Redux? Ключевые принципы Redux?](https://youtu.be/RpcB5jnJvcI?t=886)

#### Ответ

![[Pasted image 20230704192112.png|600]]

##### Введение

*Redux* - это библиотека для управления состоянием. 

*react-redux* - библиотека, которая упрощает интеграцию между React и Redux .

Для создания проекта на Redux :
~~~
~ create-react-app MyName
~ npm start

npm i redux react-redux
~~~

*В React рендеринг, действия ( actions) , логика ( reducer), state могут находиться в одном компоненте.* Для управления состояниями Redux предоставляет одно глобальное место, которое доступно из любой его части называемое "хранилищем" `store`.  Хранилище содержит состояние приложения и методы для его изменения. 

Состояние в хранилище не может быть изменено напрямую, только через действия ( `actions` ) Для отправки через actions состояний в store, используется метод [`store.dispatch()`](https://rajdee.gitbooks.io/redux-in-russian/content/docs/api/Store.html#dispatch) , который описывает, что произошло в приложении, вызывается функция  "редьюсер" ( `reducer` ), которая изменяет состояние приложения в соответствии с этим действием.

![[Pasted image 20230424203458.png]]

Без пакета **React-redux** в React приложениях выглядит не очень красиво.

##### `Provider`

Для использование store в компоненте вам необходимо передавать его в пропсы:  

```jsx
ReactDOM.render(<Main store={store} />, document.getElementById('root'));
```

И после использовать в компоненте: this.props.state. Для этого react-redux предоставляет метод Provider:  
  
```jsx
ReactDOM.render(
    <Provider store={store}>
        <Main />
    </Provider>, 
document.getElementById('root'));
```
  
Таким образом метод `connect` сможет использовать store. В противном случае вы получите ошибку: `Error: Could not find «store» in the context of «Connect(Main)». Either wrap the root component in a , or pass a custom React context provider to and the corresponding React context consumer to Connect(Main) in connect options.  `
  
Также можно передать store напрямую в компонент, не оборачивая его в Provider и это будет работать. Но лучше всё-таки используйте Provider.

Рассмотрим подробнее инструменты управления Redux .

##### 1. `actions` 

*`Actions` и `Action Creators` являются ключевыми концепциями в Redux, позволяющими управлять состоянием приложения.*

*`Actions` - это константы, описывающие событие.* 

```JSX
const ACTION_1 = "ACTION_1"; 

export default ACTION_1;
```

*`Action Creator`- это функция, которая создает `Action`. Она принимает данные и возвращает объект `Action`, который затем передается в Redux Store для обновления состояния приложения.*

`Action Creators` может содержать различные свойства, но обязательно должно быть свойство "`type"`, которое указывает на тип действия, которое нужно выполнить.

Пример `Action Creator`:
```JSX
function addTodoActionCreator(id, text) {
  return {
    type: 'ADD_TODO',
    payload: {
      id,
      text
    }
  }
}
```

В этом примере функция `addTodoActionCreator` принимает два параметра - id и text, и возвращает объект Action с типом "ADD_TODO" и данными о новой задаче.

_Вы можете использовать функцию [`bindActionCreators()`](https://rajdee.gitbooks.io/redux-in-russian/content/docs/api/bindActionCreators.html) для автоматического привязывания большого количества генераторов экшенов (action creators) к функции `dispatch()`._

Созданные таким способом функции делают сразу два действия - создание действия (action) и отправка action в dispatch()

*Action Creators позволяют абстрагироваться от создания объекта Action и упрощают процесс управления состоянием в Redux. Они также могут использоваться для асинхронных операций, таких как получение данных из API, используя middleware, такой как Redux Thunk или Redux Saga.*

##### 2. `reducer` 

*Редюсер (`reducer`) — это чистая функция, которая принимает предыдущее состояние и экшен (`state` и `action`) и возвращает следующее состояние (новую версию предыдущего).*

``` jsx
(previousState, action) => newState
```
Если previousState - underfined , то нужно вернуть первоначальный (initial) state .

Функция называется редюсером (reducer) потому, что ее можно передать в [`Array.prototype.reduce(reducer, ?initialValue)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce). 

В `reducer` никогда нельзя:
-   Непосредственно изменять то, что пришло в аргументах функции;
-   Выполнять какие-либо сайд-эффекты: обращаться к API или осуществлять переход по роутам;
-   Вызывать не чистые функции, например `Date.now()` или `Math.random()`.

Пример reducer'а, который управляет состоянием счетчика:

```jsx
function counterReducer(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}
```

В этом примере функция counterReducer принимает текущее значение состояния счетчика и объект Action, который содержит тип действия. В зависимости от типа действия, reducer обновляет состояние счетчика и возвращает новое значение.

*`Reducer` является ключевым элементом в управлении состоянием приложения и позволяет обрабатывать действия, которые изменяют состояние приложения. Он может быть объединен с другими reducer'ами с помощью функции `combineReducers` для управления состоянием всего приложения.*

**Когда вы разбиваете базовый reducer на несколько, то название каждого из них должно соответствовать полю которое он обновляет в store.**

##### 3. store 

**Стор (Store)** — это объект, который соединяет эти части вместе. 

~~~jsx
import { createStore } from 'redux'
import initReducer from './reducers'

const store = createStore(reducer, initialState);
~~~

Стор берет на себя следующие задачи:
-   содержит состояние приложения (application state);
-   предоставляет доступ к состоянию с помощью [`getState()`](https://rajdee.gitbooks.io/redux-in-russian/content/docs/api/Store.html#getState);

```JSX
store.getState()
```
вернёт значение полей хранилища. К примеру что бы посмотреть значение поля value_1 необходимо будет вызвать  

```JSX
store.getState().value_1
```

-   предоставляет возможность обновления состояния с помощью [`dispatch(action)`](https://rajdee.gitbooks.io/redux-in-russian/content/docs/api/Store.html#dispatch);
-   Обрабатывает отмену регистрации слушателей с помощью функции, возвращаемой [`subscribe(listener)`](https://rajdee.gitbooks.io/redux-in-russian/content/docs/api/Store.html#subscribelistener)

Позволяет получает нотификации об изменениях:
~~~jsx
store.subscribe(() => {
	console.log(store.getState());
});
~~~

React должен "знать" когда нужно обновлять компоненты (`store.subscribe` сообщает о том, что state обновился и обновляет UI) `store.dispatch()` используется для обновления состояния.

*`initialState`* — объект, представляющий начальное состояние хранилища. Он является вторым не обязательным аргументом метода `createStore()`.

#####  4. dispatch 

*`Dispatch` - это метод объекта Store в Redux, который используется для отправки (dispatch) действий ( actions) в Redux Store. Dispatch вызывает reducer, который обновляет состояние приложения в соответствии с переданным действием.*

В React Redux, dispatch можно использовать с помощью хука useDispatch или с помощью функции connect, которая добавляет dispatch в качестве пропса компонента.

Пример использования useDispatch:

```jsx
import { useDispatch } from 'react-redux';
import { addTodoActionCreator } from './actions';

function TodoForm() {
  const dispatch = useDispatch();

  const handleFormSubmit = (e) => {
    e.preventDefault();
    const formData = new FormData(e.target);
    const todoText = formData.get('todoText');
    dispatch(addTodoActionCreator(todoText));
  };

  return (
    <form onSubmit={handleFormSubmit}>
      <input type="text" name="todoText" />
      <button type="submit">Add Todo</button>
    </form>
  );
}
```

В этом примере компонент TodoForm использует useDispatch для получения функции dispatch из Redux Store. При отправке формы, компонент вызывает функцию handleFormSubmit, которая создает новое действие с помощью addTodoActionCreator и отправляет его в Redux Store с помощью dispatch.

Dispatch позволяет обновлять состояние приложения в Redux и является ключевым методом для взаимодействия компонентов React с Redux Store.

##### Принципы Redux

Redux имеет три основных принципа:
-   *Единое состояние:* Все состояние приложения хранится в единственном объекте-хранилище.
-   *Неизменяемость:* Состояние в хранилище не может быть изменено напрямую, только через создание нового состояния на основе старого.
-   *Чистые функции:* Редьюсеры, которые изменяют состояние в хранилище, должны быть чистыми функциями, то есть не иметь побочных эффектов и возвращать новое состояние на основе старого и действия.

##### Жизненный цикл данных в Redux

Таким образом, жизненный цикл данных в Redux включает в себя: [Поток данных (Data Flow)](https://rajdee.gitbooks.io/redux-in-russian/content/docs/basics/DataFlow.html)

- Вызов [`store.dispatch(action)`](https://rajdee.gitbooks.io/redux-in-russian/content/docs/api/Store.html#dispatch).
- **Redux-стор вызывает функцию-редюсер, который вы ему передали.**
- **Главный редюсер может комбинировать результат работы нескольких редюсеров в единственное дерево состояния приложения.**
- **Redux-стор сохраняет полное дерево состояния, которое возвращает главный редюсер.**

Подробнее: [Введение в Redux & React-redux](https://habr.com/ru/articles/498860/), [С 0 до 1. Разбираемся с Redux](https://habr.com/ru/articles/269831/), [Руководство по работе с Redux](https://habr.com/ru/companies/vk/articles/303456/)


____
#React #redux #store #action #reducer 

____

#### [[004 React + Redux|Назад]]