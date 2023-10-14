![Какие хуки были добавлены в React Router версии 5?](https://youtu.be/GZUy2i6QN7o?t=765)

#### Ответ

![[Pasted image 20230704194702.png|600]]

React Router версии 5 добавил несколько новых хуков, которые упрощают работу с маршрутизацией в React.

1. `useHistory`: Этот хук позволяет получать доступ к объекту истории, который используется для управления навигацией в React-приложении. *Он позволяет программно переходить на другую страницу, возвращаться к предыдущей странице и т.д.*

Пример использования:

```jsx
import { useHistory } from "react-router-dom";

function MyComponent() {
  let history = useHistory();

  function handleClick() {
    history.push("/about");
  }

  return (
    <button onClick={handleClick}>
      Go to About Page
    </button>
  );
}
```

2. `useLocation`: Этот хук позволяет получать доступ к текущему объекту местоположения (location), который *содержит информацию о текущем URL и других параметрах маршрута.*

Пример использования:

```jsx
import { useLocation } from "react-router-dom";

function MyComponent() {
  let location = useLocation();

  return (
    <div>
      <h1>Current Path: {location.pathname}</h1>
    </div>
  );
}
```

3. `useParams`: Этот хук позволяет получать доступ к параметрам маршрута, которые были переданы в URL. *Он позволяет легко извлекать значения параметров из URL и использовать их в компонентах.*

Пример использования:

```jsx
import { useParams } from "react-router-dom";

function MyComponent() {
  let { id } = useParams();

  return (
    <div>
      <h1>Product ID: {id}</h1>
    </div>
  );
}
```

4. `useRouteMatch`: Этот хук позволяет *получать доступ к текущему объекту маршрута (match), который содержит информацию о текущем маршруте, включая URL и параметры маршрута.*

```jsx
import { useRouteMatch } from "react-router-dom";

function MyComponent() {
  let match = useRouteMatch();

  return (
    <div>
      <h1>Current URL: {match.url}</h1>
    </div>
  );
}
```

Эти хуки позволяют удобно работать с маршрутизацией в React, упрощая доступ к текущему местоположению, параметрам и маршруту. Они значительно упрощают разработку маршрутизации в React-приложениях.

____
#React #React-router #useRouteMatch #useParams #useLocation #useHistory #hooks

____

#### [[004 React + Redux|Назад]]