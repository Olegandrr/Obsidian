![Что такое компонент-переключатель (Switching Component)?](https://youtu.be/81yRgVQ1ciM?t=265)

#### Ответ

*Компонент-переключатель (Switching Component)* - это компонент, который используется для отображения только одного дочернего компонента из нескольких, в зависимости от определенных условий.

*Компонент-переключатель обычно используется вместе с библиотекой `React Router` для управления навигацией между страницами и компонентами.* Он оборачивает множество компонентов Route и гарантирует, что только один из них будет отображен на странице в зависимости от текущего маршрута.

Пример использования компонента-переключателя в React с помощью `React Router`:

```jsx
import React from 'react';
import { BrowserRouter as Router, Switch, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';
import Contact from './Contact';

function App() {
  return (
    <Router>
      <div>
        <Switch>
          <Route exact path="/">
            <Home />
          </Route>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/contact">
            <Contact />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

export default App;
```

В этом примере компонент-переключатель Switch оборачивает множество компонентов Route, которые определяют, какой компонент должен быть отображен на странице в зависимости от текущего маршрута. Компонент Route с атрибутом exact используется для определения домашней страницы, а компоненты Route с путями /about и /contact используются для определения страниц About и Contact.

____
#React #switchingComponent #React-router 

____

#### [[004 React + Redux|Назад]]