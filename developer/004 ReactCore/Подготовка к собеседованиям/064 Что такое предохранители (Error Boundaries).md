![Что такое предохранители (Error Boundaries)?](https://youtu.be/HBSAjY-xh3k?t=36)

#### Ответ

![[Pasted image 20230704184238.png|600]]

*Предохранители (Error Boundaries)* - это механизм обработки ошибок в React-приложении, который позволяет ловить и обрабатывать ошибки, возникающие в дочерних компонентах, чтобы предотвратить падение всего приложения.

*Когда компонент внутри другого компонента возникает ошибка, React перестает обновлять интерфейс и выводит сообщение об ошибке вместо компонента. Предохранители позволяют перехватывать ошибки, возникающие в дочерних компонентах, и заменять их на другой контент, который не вызовет ошибку и не приведет к падению приложения.*

Для создания предохранителей в React необходимо определить компонент, который будет отлавливать ошибки. Для этого нужно использовать методы жизненного цикла `componentDidCatch()` или `static getDerivedStateFromError()`. В этих методах можно определить, как обрабатывать ошибки, например, заменить компонент на другой контент или отобразить панель с сообщением об ошибке.

Пример использования предохранителей (Error Boundaries) в React:

```jsx
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    console.log('Error: ', error);
    console.log('Info: ', info);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Что-то пошло не так.</h1>;
    }

    return this.props.children;
  }
}

export default ErrorBoundary;
```

В данном примере мы создаем компонент `ErrorBoundary`, который отлавливает ошибки в дочерних компонентах. Метод `getDerivedStateFromError()` вызывается, когда в дочернем компоненте произошла ошибка. Метод `componentDidCatch()` вызывается после обработки ошибки и позволяет произвести дополнительные действия, например, логирование ошибки. Если в компоненте `ErrorBoundary` возникла ошибка, то он заменяет ошибочный компонент на другой контент, например, сообщение об ошибке. Если ошибки не произошло, то компонент `ErrorBoundary` отображает дочерние компоненты при помощи `this.props.children`.

____
#React #ErrorBoundaries #componentDidCatch #getDerivedStateFromError

____

#### [[004 React + Redux|Назад]]