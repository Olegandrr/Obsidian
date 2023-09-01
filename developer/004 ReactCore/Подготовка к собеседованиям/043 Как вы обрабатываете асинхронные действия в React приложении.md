#### Ответ

Один из способов — использовать ключевые слова `async` и `await`, которые позволяют писать асинхронный код в синхронном стиле.Вот пример компонента, который выполняет асинхронный вызов API с использованием `async` и `await`: .

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

Подробнее об асинхронности можно прочитать в статье [Полное руководство по асинхронному JavaScript](https://it-dev-journal.ru/articles/polnoe-rukovodstvo-po-asinhronnomu-java-script)

____
#React

____

#### [[004 React + Redux|Назад]]