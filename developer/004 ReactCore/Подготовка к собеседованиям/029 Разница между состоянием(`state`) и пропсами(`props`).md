![Разница между состоянием(`state`) и пропсами(`props`)?](https://youtu.be/RpcB5jnJvcI?t=621)

#### Ответ

![[Pasted image 20230704174309.png|600]]

В React компонентах есть два важных концепта: состояние (`state`) и свойства (`props`).

*Свойства (`props`)* - это данные, которые передаются в компонент из вне, через атрибуты компонента. *Они являются неизменяемыми (immutable)* и могут быть доступны только для чтения внутри компонента. Свойства обычно используются для передачи данных от родительских компонентов к дочерним, и для настройки поведения компонента.

Например, в следующем коде свойство `name` передается в компонент `MyComponent`:

```jsx
function MyComponent(props) {
  return <div>Hello, {props.name}!</div>;
}

ReactDOM.render(<MyComponent name="Alice" />, document.getElementById("root"));
```

*Состояние (`state`)* - это данные, которые управляются компонентом и которые могут изменяться в процессе работы приложения. Состояние является приватным для компонента и не может быть изменено извне. Обычно состояние используется для отслеживания изменений в компоненте и для обновления пользовательского интерфейса.

Например, в следующем коде компонент `MyComponent` имеет состояние `count`, которое увеличивается при нажатии на кнопку:

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  handleClick() {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.handleClick()}>Increment</button>
      </div>
    );
  }
}

ReactDOM.render(<MyComponent />, document.getElementById("root"));
```

В целом, свойства (`props`) используются для передачи данных от родительских компонентов к дочерним, а состояние (`state`) используется для управления изменениями внутри компонента.

____
#React #state #props 

____

#### [[004 React + Redux|Назад]]