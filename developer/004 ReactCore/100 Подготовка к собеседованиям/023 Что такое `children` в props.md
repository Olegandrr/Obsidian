![Что такое `сhildren`?](https://youtu.be/HBSAjY-xh3k?t=191)

#### Ответ

![[Pasted image 20230704173937.png|600]]

В любом компоненте доступны `props.children`. Это контент между открывающим и закрывающим тегом компонента. Например:

```jsx
<Welcome>Привет, мир!</Welcome>
```

Строка `Привет, мир!` доступна в `props.children` в компоненте `Welcome`:

```jsx
function Welcome(props) {
  return <p>{props.children}</p>;
}
```

Для классовых компонентов используйте `this.props.children`:

```jsx
class Welcome extends React.Component {
  render() {
    return <p>{this.props.children}</p>;
  }
}
```

Подробнее: [props.children в React](https://codeburst.io/a-quick-intro-to-reacts-props-children-cb3d2fce4891) , [Погружаемся в работу с children на React](https://stasonmars.ru/javascript/pogruzhaemsya-v-raboty-s-children-na-react/)


____
#React #props #children 

____

#### [[004 React + Redux|Назад]]