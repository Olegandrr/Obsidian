![Что такое инверсия наследования (Inheritance Inversion)?](https://youtu.be/HBSAjY-xh3k?t=301)

#### Ответ

![[Pasted image 20230704174417.png|600]]

*Инверсия наследования (Inheritance Inversion)* - это паттерн проектирования, который используется в React для разделения логики компонента от его рендеринга. Вместо того, чтобы наследовать поведение компонента от базового класса, мы создаем компонент, который принимает функцию, которая определяет, как компонент должен быть отображен.

Этот паттерн позволяет создавать более гибкие и переиспользуемые компоненты, которые могут быть адаптированы к различным сценариям использования. 

Компоненты, использующие инверсию наследования, обычно состоят из двух частей: контейнерной части (Container) и представления (Presentation).

1. *Контейнерный компонент (Container Component)* - это компонент, который отвечает за логику и управление состоянием. Он определяет данные, которые должны быть отображены в компоненте и обрабатывает пользовательские события.
2. *Презентационный компонент (Presentation Component)* - это компонент, который принимает данные в качестве свойств и отображает их на экране. Он не имеет собственного состояния и не обрабатывает пользовательские события.

Например, представим, что у нас есть компонент `UserList`, который отображает список пользователей. Мы можем разделить его на два компонента: `UserListContainer` и `UserListPresentation`.

```jsx
class UserListContainer extends React.Component {
  constructor(props) {
    super(props);
    this.state = { users: [] };
  }

  componentDidMount() {
    fetch("/api/users")
      .then(response => response.json())
      .then(users => this.setState({ users }));
  }

  handleDeleteUser(userId) {
    // Delete user with given ID
  }

  render() {
    return (
      <UserListPresentation users={this.state.users} onDeleteUser={this.handleDeleteUser} />
    );
  }
}

function UserListPresentation(props) {
  return (
    <ul>
      {props.users.map(user => (
        <li key={user.id}>
          {user.name} <button onClick={() => props.onDeleteUser(user.id)}>Delete</button>
        </li>
      ))}
    </ul>
  );
}
```

Здесь `UserListContainer` компонент отвечает за получение данных о пользователях и управление их удалением. Он передает список пользователей и функцию удаления в `UserListPresentation` компонент, который отображает список пользователей и рендерит кнопку удаления для каждого пользователя.

____
#React #container #presentation

____

#### [[004 React + Redux|Назад]]