#### Ответ

##### `async \ await`

Один из способов — использовать ключевые слова `async` и `await`, которые позволяют писать асинхронный код в синхронном стиле.Вот пример компонента, который выполняет асинхронный вызов API с использованием `async` и `await`: 

```javascript
import React, { useState, useEffect } from 'react';

function MyComponent() {
 const [data, setData] = useState(null);

 useEffect(() => {
   async function fetchData() {
     const response = await fetch('https://example.com/get-data');
     const data = await response.json();
     setData(data);
   }
   fetchData();
 }, []);

 return (
   <div>
     {data ? (
       <div>{data.message}</div>
     ) : (
       <div>Loading...</div>
     )}
   </div>
 );
}
```

##### `axios || fetch`

Другой способ обработки асинхронных функций в React — использование библиотеки, такой как `axios` или `fetch`, для выполнения API вызовов. Вот пример использования `axios`:

```javascript
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function MyComponent() {
 const [data, setData] = useState(null);

 useEffect(() => {
   async function fetchData() {
     const response = await axios.get('https://example.com/get-data');
     setData(response.data);
   }
   fetchData();
 }, []);

 return (
   <div>
     {data ? (
       <div>{data.message}</div>
     ) : (
       <div>Loading...</div>
     )}
   </div>
 );
}
```

Подробнее: [Полное руководство по асинхронному JavaScript](https://it-dev-journal.ru/articles/polnoe-rukovodstvo-po-asinhronnomu-java-script)

Если про `fetch` было рассказано ранее, то поднимем тему, что такое `axios`, преимущества axios перед fetch.

###### `fetch` vs `axios`

`Axios` — это широко известная JavaScript-библиотека. Она представляет собой HTTP-клиент, основанный на промисах и предназначенный для браузеров и для Node.js.

|                           | **fetch**                                        | **axios**                                                                                |
| ------------------------- | ------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| **Использование**         | встроенный объект в JS                           | сторонняя библиотека                                                                     |
| **Базовый синтаксис**     | более объемный код                               | менее объёмный код                                                                       |
| **Множественные запросы** | promise.all                                      | axios.all                                                                                |
| **Поддержка браузера**    | ---                                              | имеет лучшую обратную поддержку браузеров.                                               |
| **HTTP-перехватчики**     | не предоставляет способ сделать это по умолчанию | обеспечивает простой и легкий способ использования перехватчиков **HTTP**                |
| **Размер связки**         | встроен                                          | добавит некоторую дополнительную зависимость, поскольку это сторонняя библиотека (371КБ) |
| **Безопасность**          | тоже имеет встроенную защиту (но сложнее)        | имеет встроенную защиту **XSRF** (подделка межсайтовых запросов)                         |
| **Обработка ошибок**      | не выдаёт сведения о сетевых ошибках             | выдаёт сведения о сетевых ошибках                                                        |
| **Статус загрузки**       | нет такой возможности                            | встроенная возможность                                                                   | 

Подробнее: [Axios или Fetch: чем пользоваться в 2019 году?](https://habr.com/ru/companies/ruvds/articles/477286/)

____
#React #fetch #axios #AJAX #promise #async #await #XSRF 

____

#### [[004 React + Redux|Назад]]