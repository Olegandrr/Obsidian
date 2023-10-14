![Что такое «бурение пропсов» (Prop Drilling)? Как его избежать?](https://youtu.be/81yRgVQ1ciM?t=532)

#### Ответ

![[Pasted image 20230704174005.png|600]]

*"Бурение пропсов" (Prop Drilling)* - это ситуация, когда компоненты передают свойства (`props`) через несколько уровней вложенности, чтобы достичь глубоко вложенных компонентов. Это может привести к необходимости передавать одни и те же свойства через несколько компонентов в длинной цепочке вложенности, что усложняет понимание кода и ухудшает его читаемость.

Пример:

```jsx
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <Header count={count} />
      <Content count={count} setCount={setCount} />
    </div>
  );
}

function Header(props) {
  return <h1>Count: {props.count}</h1>;
}

function Content(props) {
  return (
    <div>
      <Counter count={props.count} setCount={props.setCount} />
    </div>
  );
}

function Counter(props) {
  const handleClick = () => {
    props.setCount(props.count + 1);
  };

  return (
    <div>
      <p>Current count: {props.count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
}
```

В этом примере компонент `App` передает свойство `count` и функцию `setCount` через компонент `Content` до компонента `Counter`. Это приводит к "бурению пропсов", так как свойства передаются через несколько уровней вложенности.

Для решения этой проблемы можно использовать более продвинутые методы передачи данных между компонентами, такие как `Context API` или `Redux`. Эти методы позволяют передавать данные и функции между компонентами без необходимости передавать их через несколько уровней вложенности.

____
#React #props #propsDrilling #Context 

____

#### [[004 React + Redux|Назад]]