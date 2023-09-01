#### Ответ

Если вы хотите получить доступ к `this.props` в `constructor()`, тогда вы должны передать props методу `super()`.

**Использование  `super(props)`:**

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log(this.props); // { name: 'John', ... }
  }
}
```

**Использование `super()`:**

```js
class MyComponent extends React.Component {
  constructor(props) {
    super();
    console.log(this.props); // undefined
	  }
}
```

Вне `constructor()` оба будут отображать одинаковое значение для `this.props`.

____
#React #constructor #super #props

____

#### [[004 React + Redux|Назад]]