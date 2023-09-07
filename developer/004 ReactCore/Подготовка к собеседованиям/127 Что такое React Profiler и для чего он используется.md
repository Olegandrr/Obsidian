#### Ответ

React `Profiler` - это инструмент для измерения затрат на рендеринг в приложении React. Он помогает разработчикам идентифицировать части приложения, которые работают медленно и могут быть оптимизированы.

Компонент `Profiler` может быть добавлен в любом месте дерева компонентов, чтобы измерить затраты на его рендеринг. Например, приведенный ниже код демонстрирует, как компонент `Profiler` используется для измерения затрат на рендеринг компонента `Navigation` и его потомков:

```jsx
render(
  <App>
    <Profiler id="Navigation" onRender={callback}>
      <Navigation {...props} />
    </Profiler>
    <Main {...props} />
  </App>
);
```

Подробнее: [Профилирование производительности React-приложений](https://habr.com/ru/companies/ruvds/articles/497988/), [React Profiler](https://ru.legacy.reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html)

____
#React #Profiler

____

#### [[004 React + Redux|Назад]]