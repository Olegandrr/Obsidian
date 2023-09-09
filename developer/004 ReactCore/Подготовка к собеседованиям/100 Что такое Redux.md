![Что такое Redux? Ключевые принципы Redux?](https://youtu.be/RpcB5jnJvcI?t=886)

![](https://www.youtube.com/watch?v=KSgp8gn8v2I)
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

Состояние в хранилище не может быть изменено напрямую, только через  `actions` . Для отправки через `actions` состояний в `store`, используется метод [`store.dispatch()`](https://rajdee.gitbooks.io/redux-in-russian/content/docs/api/Store.html#dispatch) , который описывает, что произошло в приложении, вызывается `reducer` , который изменяет состояние приложения в соответствии с этим действием.

![[Pasted image 20230424203458.png]]

Без пакета **react-redux** в React приложениях выглядит не очень красиво.

Для использование `store` в компоненте вам необходимо передавать его в пропсы:  

```jsx
ReactDOM.render(<Main store={store} />, document.getElementById('root'));
```

И после использовать в компоненте: `this.props.state`.  Для этого `react-redux` предоставляет метод `Provider`:  
  
```jsx
ReactDOM.render(
    <Provider store={store}>
        <Main />
    </Provider>, 
document.getElementById('root'));
```
  
Таким образом метод `connect` сможет использовать `store`. В противном случае вы получите ошибку: `Error: Could not find «store» in the context of «Connect(Main)». Either wrap the root component in a , or pass a custom React context provider to and the corresponding React context consumer to Connect(Main) in connect options.  `
  
Также можно передать `store` напрямую в компонент, не оборачивая его в `Provider` и это будет работать. Но лучше всё-таки используйте Provider.

##### Принципы Redux

Redux имеет три основных принципа:
-   *Единое состояние:* Все состояние приложения хранится в единственном объекте-хранилище.
-   *Неизменяемость:* Состояние в хранилище не может быть изменено напрямую, только через создание нового состояния на основе старого.
-   *Чистые функции:* Редьюсеры, которые изменяют состояние в хранилище, должны быть чистыми функциями, то есть не иметь побочных эффектов и возвращать новое состояние на основе старого и действия.

Подробнее: [Введение в Redux & React-redux](https://habr.com/ru/articles/498860/), [С 0 до 1. Разбираемся с Redux](https://habr.com/ru/articles/269831/), [Руководство по работе с Redux](https://habr.com/ru/companies/vk/articles/303456/) ,  [Поток данных (Data Flow)](https://rajdee.gitbooks.io/redux-in-russian/content/docs/basics/DataFlow.html).

____
#React #redux #store #action #reducer 

____

#### [[004 React + Redux|Назад]]