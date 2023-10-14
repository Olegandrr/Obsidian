#### Ответ

Да, безопасно использовать метод `setState()` внутри метода `componentWillMount()`. Однако, в то же время, рекомендуется избегать асинхронной инициализации в методе жизненного цикла `componentWillMount()`. *Метод `componentWillMount()` вызывается непосредственно перед монтированием компонента. Он вызывается до метода `render()`, поэтому установка состояния в этом методе не приведет к повторному рендерингу.* Следует избегать введения любых побочных эффектов или подписок в этом методе. Необходимо убедиться, что асинхронные вызовы для инициализации компонента происходят в методе `componentDidMount()` вместо `componentWillMount()`.

```js
componentDidMount() {
  axios.get(`api/todos`)
    .then((result) => {
      this.setState({
        messages: [...result.data]
      })
    })
}
```

____
#React #setState #compomemtWillMount #componentDidMount 

____

#### [[004 React + Redux|Назад]]