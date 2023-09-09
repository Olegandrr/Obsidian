____

![](https://www.youtube.com/watch?v=lvIfuti1sug)

![](https://www.youtube.com/watch?v=j_RIqH9NwW0)

#### Ответ

*React-routing (роутинг в React)* - это процесс управления навигацией между страницами и компонентами в React-приложении. 
*Роутинг позволяет динамически изменять содержание страницы, не перезагружая всю страницу, а только обновляя её содержимое в соответствии с выбранным маршрутом.*

Роутинг обычно реализуется с помощью библиотеки `React Router`. Она предоставляет удобный API для определения маршрутов и управления навигацией в React-приложении.

Основные компоненты, используемые в `React Router`, включают в себя:
1. *BrowserRouter:* Компонент, который используется для определения корня маршрутизации в приложении. Он обычно обертывает всё приложение.
2. *Route:* Компонент, который определяет, какой компонент должен быть отображен на странице в зависимости от текущего маршрута. Он принимает путь (path) и компонент, который должен быть отображен.
3. *Switch:* Компонент, который используется для обертывания множества маршрутов. Он гарантирует, что только один маршрут будет отображен на странице в зависимости от текущего маршрута.
4. *Link:* Компонент, который используется для создания ссылок на различные маршруты в приложении. Он позволяет пользователям переходить между страницами без перезагрузки всей страницы.

Пример использования React Router:

```jsx
import React from 'react';
import { BrowserRouter as Router, Route, Switch, Link } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Contact from './components/Contact';

function App() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
              <Link to="/contact">Contact</Link>
            </li>
          </ul>
        </nav>
        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/contact">
            <Contact />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

export default App;
```

В этом примере используется React Router для создания маршрутизации между компонентами Home, About и Contact. `BrowserRouter` оборачивает всё приложение, а компоненты Route определяют, какой компонент должен быть отображен на странице в зависимости от текущего маршрута. Link используется для создания ссылок на различные маршруты в приложении.

Подробнее: [Простой туториал React Router v4](https://habr.com/ru/articles/329996/)

____
#React #React-routing 

____

#### [[004 React + Redux|Назад]]