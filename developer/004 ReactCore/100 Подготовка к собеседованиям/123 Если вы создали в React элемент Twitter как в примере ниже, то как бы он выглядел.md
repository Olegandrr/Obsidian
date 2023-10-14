#### Ответ

```jsx
<Twitter username='tylermcginnis33'>  
  {(user) => user === null  
    ? <Loading />  
    : <Badge info={user} />}  
</Twitter>import React, { Component, PropTypes } from 'react'  
import fetchUser from 'twitter'
// fetchUser принимает имя пользователя и возвращает promise  
// который резолвится с данными пользователя
class Twitter extends Component {  
  // закончите код здесь  
}
```

Если вы не очень хорошо знакомы с шаблоном _render callback_, это может показаться немного странным. В этом шаблоне компонент получает функцию в качестве своего потомка. Обратите внимание, что находится внутри тега `_<Twitter>`_ выше. Потомок компонента Twitter является функцией. Это означает то, что в данной реализации компонента Twitter нам необходимо обратиться к _props.children_ как к функции.

Вот как я вижу это решение:

```jsx
import React, { Component, PropTypes } from 'react'  
import fetchUser from 'twitter'class Twitter extends Component {  
  state = {  
    user: null,  
  }  
  static propTypes = {  
    username: PropTypes.string.isRequired,  
  }  
  componentDidMount () {  
    fetchUser(this.props.username)  
      .then((user) => this.setState({user}))  
  }  
  render () {  
    return this.props.children(this.state.user)  
  }  
}
```
Обратите внимание, что, как упоминал выше, я обращаюсь к _props.children_ как к функции, вызывая ее и передавая пользователя.

В этом шаблоне хорошо то, что мы выделили наш родительский компонент из нашего дочернего компонента. Родительский компонент управляет состоянием и потребитель родительского компонента может решить каким образом они хотели бы использовать переданные аргументы в их интерфейсе, полученные из родительского.

Чтобы продемонстрировать это, давайте примем, что в другом файле мы хотим отрисовать _Profile_ вместо _Badge_, и так как мы используем шаблон _render callback_, мы можем менять окружение интерфейса без изменения нашей реализации родительского компонента _Twitter_.

```jsx
<Twitter username='tylermcginnis33'>  
  {(user) => user === null  
    ? <Loading />  
    : <Profile info={user} />}  
</Twitter>
```


____
#React

____

#### [[004 React + Redux|Назад]]