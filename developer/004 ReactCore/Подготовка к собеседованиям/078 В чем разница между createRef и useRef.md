#### Ответ

`createRef` и `useRef` - это два разных инструмента в React для работы с рефами (refs), которые позволяют получать доступ к DOM элементам и другим компонентам.

*`createRef`* - это метод класса React, который позволяет создавать рефы (refs) для доступа к DOM элементам и другим компонентам в методах жизненного цикла компонента.

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }

  render() {
    return <div ref={this.myRef}>Hello, World!</div>;
  }
}
```

В этом примере, `createRef()` используется для создания рефа `myRef`. Реф передается в DOM элемент через атрибут `ref`.

*`useRef`* - это хук в React, который позволяет создавать рефы (refs) для доступа к DOM элементам и другим компонентам в функциональных компонентах.

```jsx
function MyComponent() {
  const myRef = useRef(null);
  return <div ref={myRef}>Hello, World!</div>;
}
```

В этом примере, `useRef()` используется для создания рефа `myRef`. Реф передается в DOM элемент через атрибут `ref`.

Таким образом, основная разница между `createRef` и `useRef` заключается в том, что `createRef` используется в классовых компонентах, а `useRef` - в функциональных компонентах с использованием хуков. Оба инструмента могут быть полезными для доступа к DOM элементам и другим компонентам в React.

____
#React #createRef #useRef #Hooks 

____

#### [[004 React + Redux|Назад]]