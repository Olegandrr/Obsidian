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

##### `React Query`

**React Query** - библиотека для получения, кэширования, синхронизации и обновления "серверного" состояния в React-приложениях.

```
yarn add react-query
# или
npm i react-query
```

Ключевыми концепциями `React Query` являются:
- Запросы (queries)
- Мутации (mutations)
- Инвалидация (аннулирование, признание недействительным) запроса (query invalidation), его кэша

Библиотека `react-query` позволяет работать запросами к серверу, предоставляет доступ данным, позволяет задавать порядок запросов.. Однако для того чтобы с этим работать надо разделить весь стэйт который есть в redux на 2 части. Первая — это как раз данные, полученные с сервера. Вторая — это все остальное.

Подключается  примерно так:

```jsx
import { QueryClient, QueryClientProvider } from 'react-query';
import { ReactQueryDevtools } from 'react-query/devtools';
 
import { CitiesProvider } from './store/cities/cities-provider';
 
const queryClient = new QueryClient();
 
ReactDOM.render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <CitiesProvider>
        <App />
```

Простой пример использования:

```jsx
const queryCities = useQuery('cities', fetchCitiesFunc);
const cities = queryCities.data || [];
```

Первый параметр `'cities'` это ключ строка, которая должна быть уникальной для каждого запроса. Второй - это функция, которая возвращает Promise, который резолвит данные или отдает ошибку. Также можно передать третьим параметром объект с настройками.

*`useQuery()` возвращает объект `UseQueryResult()`, который содержит данные о состоянии запроса, ошибку или данные*

```jsx
const { isLoading, isIdle, isError, data, error } = useQuery(..
```

Для выполнения последовательных запросов мне показалось удобным написать отдельный хук

```jsx
export function useCurrentWeather(): WeatherCache {
  const { currentCity } = useContext(СitiesContext);
 
 // запрашиваем список городов
  const queryCities = useQuery('cities', fetchCitiesFunc, {
     refetchOnWindowFocus: false,
    staleTime: 1000 * 60 * 1000,
  });
  const citiesRu = queryCities.data || [];
 
// ищем идентификатор текущего города.. 
 const city = citiesRu.find((city) => {
    if (city === undefined) return false;
    const { id: elId } = city;
    if (currentCity === elId) return true;
    return false;
  });
 
  const { id: weatherId } = city ?? {};
 
 // запрашиваем текущую погоду
  const queryWeatherCity = useQuery(
    ['weatherCity', weatherId],
    () => fetchWeatherCityApi(weatherId as number),
    {
      enabled: !!weatherId,
      staleTime: 5 * 60 * 1000,
    },
  );
 
  const { coord } = queryWeatherCity.data ?? {};
 
 // запрашиваем прогноз по координатам из предыд. запроса
  const queryForecastCity = useQuery(
    ['forecastCity', coord],
    () => fetchForecastCityApi(coord as Coord),
    {
      enabled: !!coord,
      staleTime: 5 * 60 * 1000,
    },
  );
 
  return {
    city,
    queryWeatherCity,
    queryForecastCity,
  };
}
```

У `react-query` есть возможность вывести окошко инструментов разработчика. Оно немного похоже на окно Redux, но появляется в виде фиксированного окошка поверх приложения(можно закрыть и останется только кнопка) 

![Окно инструментов разработчика](https://habrastorage.org/r/w1560/getpro/habr/upload_files/382/d0a/9d3/382d0a9d362867d2f527b1187488b829.png "Окно инструментов разработчика")

- `useQueries` позволяет динамически формировать массив запросов. Это нужно т.к. мы не можем опционально вызывать хуки `useQuery`.

```jsx
const userQueries = useQueries(
  users.map(user => {
    return {
      queryKey: ['user', user.id],
      queryFn: () => fetchUserById(user.id),
    }
  })
```

Подробнее: [Кэш или стэйт, пробуем React-query](https://habr.com/ru/articles/557620/), [React Query](https://reactdev.ru/libs/react-query/)

____
#React #fetch #axios #AJAX #promise #async #await #XSRF #React-Query #useQuery

____

#### [[004 React + Redux|Назад]]