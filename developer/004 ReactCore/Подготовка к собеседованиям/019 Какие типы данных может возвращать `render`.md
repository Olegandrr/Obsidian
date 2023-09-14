![Какие типы данных может возвращать `render`?](https://youtu.be/DgevxmyzymQ?t=90)

#### Ответ

![[Pasted image 20230704173902.png|600]]

Метод `render()` возвращает JSX-элементы, которые представляют собой виртуальное представление компонента. JSX может быть представлен различными типами данных, такими как:

1. *Элементы*
2. *Строки и числа
3. *Массивы*
4. *`null` и `false`*
5. *Порталы (`Portals`)
6. *`React.Fragment`*


##### `Render Props`

*`Render Props` — это функция, которая сообщает компоненту что необходимо рендерить.*

```jsx
<DataProvider
  render={(data) => <h1>Привет, {data.target}</h1>}
/>
```

Важно запомнить, что из названия паттерна «рендер-проп» вовсе не следует, что для его использования _вы должны обязательно называть проп `render`_. На самом деле, [_любой_ проп, который используется компонентом и является функцией рендеринга, технически является и «рендер-пропом»](https://cdb.reacttraining.com/use-a-render-prop-50de598f11ce).

Подробнее: [Что такое Render Props](https://reactdev.ru/archive/react16/render-props/#be-careful-when-using-render-props-with-reactpurecomponent),  [Рендер-пропсы](https://ru.reactjs.org/docs/render-props.html)

____
#React #render #JSX #portals 

____

#### [[004 React + Redux|Назад]]