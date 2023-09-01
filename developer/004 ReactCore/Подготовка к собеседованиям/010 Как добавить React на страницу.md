#### Ответ

1. Для того, чтобы работать в #React необходимо применить скрипт:
```jsx
	npx create-react-app my-app
```

И подготовить директорию к работе, удалив шаблонные файлы проекта.

2. Привязываем терминал к проекту
~~~jsx
cd my-app
~~~

3. Удаляем лишние файлы и подготавливаем наш шаблон к работе

4. Импортируем библиотеку React
~~~jsx
import React, { Component } from 'react';
~~~

5. Импортируем библиотеку react-dom
~~~jsx
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'));
~~~

createRoot - корневой DOM-узел, тк через него мы управляем React содержимым.

____
#React 

____

#### [[004 React + Redux|Назад]]