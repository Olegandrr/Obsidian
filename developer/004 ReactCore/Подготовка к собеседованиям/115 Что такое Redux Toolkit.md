![](https://www.youtube.com/watch?v=gPmYTqGPDWA)

![](https://www.youtube.com/watch?v=C0fBnil_Im4)

#### Ответ

Почитать документацию: [Redux Toolkit](https://redux-toolkit.js.org/introduction/getting-started)
##### Введение

*Redux Toolkit* - это библиотека, которая предоставляет набор утилит для упрощения разработки Redux-приложений. Релиз библиотеки состоялся в 2019 году и официально поддерживается разработчиками Redux. 

Redux Toolkit выполняет следующие функции:
- помогает быстро начать использовать Redux;
- упрощает работу с типичными задачами и кодом Redux;
- позволяет использовать лучшие практики Redux по умолчанию;
- предлагает решения, которые уменьшают недоверие к бойлерплейтам.

##### Методы Redux Toolkit

Вот некоторые основные функции и концепции Redux Toolkit:

- **[#configureStore](https://habr.com/ru/companies/inobitec/articles/481288/#configureStore)**— функция, предназначенная упростить процесс создания и настройки хранилища;
- **[#createReducer](https://habr.com/ru/companies/inobitec/articles/481288/#createReducer)**— функция, помогающая лаконично и понятно описать и создать редьюсер;
- **[#createAction](https://habr.com/ru/companies/inobitec/articles/481288/#createAction)**— возвращает функцию создателя действия для заданной строки типа действия;
- **[#createSlice](https://habr.com/ru/companies/inobitec/articles/481288/#createSlice)**— объединяет в себе функционал createAction и createReducer;
- **createSelector** — функция из библиотеки [Reselect](https://github.com/reduxjs/reselect), переэкспортированная для простоты использования.

*Redux Toolkit полностью интегрирован с TypeScript.* 
Более подробную информацию об этом можно получить из раздела [Usage With TypeScript](https://redux-toolkit.js.org/usage/usage-with-typescript/) официальной документации.

###### `configureStore()`

Чтобы упростить процесс конфигурации хранилища используют `configureStore()`. 

```jsx
import { configureStore } from '@reduxjs/toolkit'  
  
import rootReducer from './reducers'  
  
const store = configureStore({ reducer: rootReducer })  
// The store now has redux-thunk added and the Redux DevTools Extension is turned on
```

В качестве входных параметров функция `configureStore` принимает объект со следующими свойствами:
- `reducer` — набор пользовательских редьюсеров,
- `middleware` — опциональный параметр, задающий массив мидлваров, предназначенных для подключения к хранилищу,
- `devTools` — параметр логического типа, позволяющий включить установленное в браузер расширение Redux DevTools (значение по умолчанию — true),
- `preloadedState` — опциональный параметр, задающий начальное состояние хранилища,
- `enhancers` — опциональный параметр, задающий набор усилителей.

Данный инструмент позволяет автоматически комбинировать редьюсеры, добавить мидлвары (по умолчанию включает redux-thunk), а также использовать расширение `Redux DevTools`. 

```jsx
// file: todos/todosReducer.ts noEmit
import type { Reducer } from '@reduxjs/toolkit'
declare const reducer: Reducer<{}>
export default reducer

// file: visibility/visibilityReducer.ts noEmit
import type { Reducer } from '@reduxjs/toolkit'
declare const reducer: Reducer<{}>
export default reducer

// file: store.ts
import { configureStore } from '@reduxjs/toolkit'

// We'll use redux-logger just as an example of adding another middleware
import logger from 'redux-logger'

// And use redux-batched-subscribe as an example of adding enhancers
import { batchedSubscribe } from 'redux-batched-subscribe'

import todosReducer from './todos/todosReducer'
import visibilityReducer from './visibility/visibilityReducer'

const reducer = {
  todos: todosReducer,
  visibility: visibilityReducer,
}

const preloadedState = {
  todos: [
    {
      text: 'Eat food',
      completed: true,
    },
    {
      text: 'Exercise',
      completed: false,
    },
  ],
  visibilityFilter: 'SHOW_COMPLETED',
}

const debounceNotify = _.debounce((notify) => notify())

const store = configureStore({
  reducer,
  middleware: (getDefaultMiddleware) => getDefaultMiddleware().concat(logger),
  devTools: process.env.NODE_ENV !== 'production',
  preloadedState,
  enhancers: [batchedSubscribe(debounceNotify)],
})

// Store был создан с такими параметрами:  
// - срезы редукторов были автоматически переданы в combineReducers() 
// - библиотеки redux-thunk и redux-logger были добавлены как middleware 
// - расширение Redux DevTools было отключено для продакшена  
// - middleware, пакетное подписывание и улучшители дебаговых инструментов были объединены вместе
```

Для получения наиболее популярного списка мидлваров можно воспользоваться специальной функцией `getDefaultMiddleware`, также входящей в состав Redux Toolkit. Данная функция возвращает массив с включенными по умолчанию в библиотеку Redux Toolkit мидлварами. Перечень этих мидлваров отличается в зависимости от того, в каком режиме выполняется ваш код. В production режиме массив состоит только из одного элемента — thunk. В режиме development на момент написания статьи список пополняется следующими мидлварами:
- `serializableStateInvariant` — инструмент, специально разработанный для использования в Redux Toolkit и предназначенный для проверки дерева состояний на предмет наличия несериализуемых значений, таких как функции, Promise, Symbol и другие значения, не являющиеся простыми JS-данными;
- `immutableStateInvariant` — мидлвар из пакета [redux-immutable-state-invariant](https://www.npmjs.com/package/redux-immutable-state-invariant), предназначенный для обнаружения мутаций данных, содержащихся в хранилище.

###### `createReducer()`

Функция `createReducer()` похожа на функцию создания поисковой таблицы из документации по `Redux`. В ней используется библиотека `immer`, что позволяет писать "мутирующий" код, обновляющий состояние иммутабельно. Это защищает от непреднамеренного мутирования состояния в редукторе.

Любой редуктор, в котором используется инструкция `switch`, может быть преобразован с помощью `createReducer()`. Каждый `case` становится ключом объекта, передаваемого в `createReducer()`. Иммутабельные обновления, такие как распаковка объектов или копирование массивов, могут быть преобразованы в "мутации". Но это не обязательно: можно оставить все как есть.

Ниже приводится пример использования `createReducer()`. Начнем с типичного редуктора для списка задач, в котором используется инструкция `switch` и иммутабельные обновления:

```jsx
function todosReducer(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO': {
      return state.concat(action.payload);
    }
    case 'TOGGLE_TODO': {
      const { index } = action.payload;
      return state.map((todo, i) => {
        if (i !== index) return todo;

        return {
          ...todo,
          completed: !todo.completed,
        };
      });
    }
    case 'REMOVE_TODO': {
      return state.filter(
        (todo, i) => i !== action.payload.index
      );
    }
    default:
      return state;
  }
}
```

_Обратите внимание_, что мы вызываем `state.concat()` для получения копии массива с новой задачей, `state.map()` также для получения копии массива, и используем оператор `spread` для создания копии задачи, подлежащей обновлению.

С помощью `createReducer()` мы можем сократить приведенный пример следующим образом:

```jsx
const todosReducer = createReducer([], (builder) => {
  builder
    .addCase('ADD_TODO', (state, action) => {
      // "мутируем" массив, вызывая push()
      state.push(action.payload);
    })
    .addCase('TOGGLE_TODO', (state, action) => {
      const todo = state[action.payload.index];
      // "мутируем" объект, перезаписывая его поле `completed`
      todo.completed = !todo.completed;
    })
    .addCase('REMOVE_TODO', (state, action) => {
      // мы по-прежнему можем использовать иммутабельную логику обновления состояния
      return state.filter(
        (todo, i) => i !== action.payload.index
      );
    });
});
```

Возможность "мутировать" состояние особенно полезна при необходимости обновления глубоко вложенных свойств. Например, такой код:

```jsx
case 'UPDATE_VALUE':
  return {
    ...state,
    first: {
      ...state.first,
      second: {
        ...state.first.second,
        [action.someId]: {
          ...state.first.second[action.someId],
          fourth: action.someValue
        }
      }
    }
  }

```

Можно упростить так:

```jsx
updateValue(state, action) {
  const { someId, someValue } = action.payload
  state.first.second[someId].fourth = someValue
}

```

Функция `createReducer()` может быть очень полезной, но следует помнить о том, что:

- "Мутирующий" код правильно работает только внутри `createReducer()`
- `Immer` не позволяет смешивать "мутирование" черновика (`draft`) состояния и возвращение нового состояния

###### `createAction()`

Написание создателей операции вручную может быть утомительным. `Redux Toolkit` предоставляет функцию `createAction()`, которая генерирует создателя операции с указанным типом операции и преобразует переданные аргументы в поле `payload`:

```jsx
const addTodo = createAction('ADD_TODO');
addTodo({ text: 'Buy milk' });
// { type : "ADD_TODO", payload : {text : "Buy milk"}} )

```

`createAction()` также принимает аргумент-колбек `prepare`, позволяющий кастомизировать результирующее поле `payload` и добавлять поле `meta`, при необходимости.

Для определения того, как должно быть обновлено состояние, редукторы полагаются на тип операции. Обычно, это делается посредством раздельного определения типов и создателей операции. `createAction()` позволяет упростить данный процесс.

Во-первых, `createAction()` перезаписывает метод `toString()` генерируемых создателей. Это означает, что создатель может использовать в качестве ссылки на "тип операции", например, в ключах, передаваемых в `builder.addCase()` или объектной нотации `createReducer()`.

Во-вторых, тип операции также определяется как поле `type` создателя.

```jsx
const actionCreator = createAction('SOME_ACTION_TYPE');

console.log(actionCreator.toString());
// SOME_ACTION_TYPE

console.log(actionCreator.type);
// SOME_ACTION_TYPE

const reducer = createReducer({}, (builder) => {
  // Здесь будет автоматически вызван `actionCreator.toString()`
  // Кроме того, при использовании TypeScript, будет правильно предложен (предположен) тип операции
  builder.addCase(actionCreator, (state, action) => {});

  // Или вы можете указать поле `type`
  // В этому случае, при использовании TypeScript, тип операции предложен не будет
  builder.addCase(
    actionCreator.type,
    (state, action) => {}
  );
});
```

Это означает, что нам не нужно создавать отдельную переменную для типа операции или дублировать название и значение типа, например: `const SOME_ACTION_TYPE = 'SOME_ACTION_TYPE'`.

К сожалению, неявного приведения к строке не происходит в инструкции `switch`. Приходится делать это вручную:

```jsx
const actionCreator = createAction('SOME_ACTION_TYPE');

const reducer = (state = {}, action) => {
  switch (action.type) {
    // ошибка
    case actionCreator: {
      break;
    }
    // правильно
    case actionCreator.toString(): {
      break;
    }
    // так тоже работает
    case actionCreator.type: {
      break;
    }
  }
};
```

При использовании `Redux Toolkit` с `TypeScript`, принимайте во внимание, что компилятор `TypeScript` может не осуществлять неявного преобразования в строку, когда создатель используется как ключ объекта. В этом случае также может потребоваться прямое указание типа создателя (`actionCreator as string`) или использование поля `type` в качестве ключа объекта.

###### `createSlice()`

`createSlice()` автоматически генерирует типы и создателей операции на основе переданного названия редуктора:

```jsx
const postsSlice = createSlice({
  name: 'posts',
  initialState: [],
  reducers: {
    createPost(state, action) {},
    updatePost(state, action) {},
    deletePost(state, action) {},
  },
});

console.log(postsSlice);
/*
{
  name: 'posts',
  actions : {
      createPost,
      updatePost,
      deletePost,
  },
  reducer
}
*/

const { createPost } = postsSlice.actions;

console.log(
  createPost({ id: 123, title: 'Привет, народ!' })
);
// { type : 'posts/createPost', payload : { id : 123, title : 'Привет, народ!' } }
```

`createSlice()` анализирует функции, определенные в поле `reducers`, создает редуктор для каждого случая и генерирует создателя, использующего название редуктора в качестве типа операции. Таким образом, редуктор `createPost` становится типом операции `posts/createPost`, а создатель `createPost()` возвращает операцию с этим типом.

Обычно, мы определяем часть и экспортируем создателей и редукторы:

```jsx
const postsSlice = createSlice({
  name: 'posts',
  initialState: [],
  reducers: {
    createPost(state, action) {},
    updatePost(state, action) {},
    deletePost(state, action) {},
  },
});

// Извлекаем объект с создателями и редуктор
const { actions, reducer } = postsSlice;
// Извлекаем и экспортируем каждого создателя по названию
export const {
  createPost,
  updatePost,
  deletePost,
} = actions;
// Экпортируем редуктор по умолчанию или по названию
export default reducer;
```

###### Список источников

Подробнее: [Redux Toolkit](https://reactdev.ru/libs/redux-toolkit/#_46), [Redux Toolkit - официальная документация](https://redux-toolkit.js.org/) , [Redux Toolkit как средство эффективной Redux-разработки](https://habr.com/ru/companies/inobitec/articles/481288/) 

##### `RTK Query`

Почитать документацию: [RTK Query](https://redux-toolkit.js.org/tutorials/rtk-query)

###### Введение

**RTK Query** — это мощный инструмент для получения и кэширования данных. *Он предназначен для упрощения распространенных случаев загрузки данных в веб-приложении, избавляя от необходимости вручную писать логику загрузки и кэширования данных.*

`RTK Query` — это дополнительный аддон, включенный в пакет `Redux Toolkit`, и его функциональность построена поверх других API в Redux Toolkit.

###### Особенности `RTK Query`

- Под капотом RTK Query использует `createSlice` и `createAsyncThunk`, которые предоставляет API Redux Toolkit. 
- В RTQ Query взаимодействие с API задается с помощью endpoint, которые определены в момент инициализации API (метод createApi, о котором пойдет речь ниже);
- RTK Query автоматически создает хуки, исходя из заданных эндпоинтов. Данные хуки могут быть использованы непосредственно в React компонентах для загрузки/отображения/изменения данных. Механизм взаимодействия с API инкапсулирован. 
- RTK Query поддерживает кэширование из коробки. 
- Позволяет решить проблему дедубликации запросов, например, если два компонента на одной странице совершают один и тот же запрос к API, выполнен будет лишь один запрос.

###### Недостатки `RTK Query`

Недостатки:
- В реальном проекте может быть несколько файлов с различными блоками API, и в этом случае возникает вопрос, как связать всё вместе.
- Проблема решается тем, что все действия по загрузке, мутированию обновлению кэша, инвалидации в RTQ Query могут быть вызваны с использованием dispatch из любого места приложения.
- Система тегов непроста и не так прозрачна, как у альтернатив.

###### `RTK Query` на практике

Начнем с создания с так называемого `“API Slice”`, в котором определим базовый URL сервера и эндпоинты, с которым нужно будет взаимодействовать.  

Определим три главных параметра:  
1. `reducerPath`. Уникальный ключ, который будет добавлен в store
2. `baseQuery`. Параметр baseQuery отвечает за непосредственное взаимодействие с API. В состав RTK Query входит инструмент под названием `fetchBaseQuery`, представляющий собой легковесную обертку над fetch, подходящий для большинства операций по работе с API.
3. `endPoints`. Это набор взаимодействий с API. Существует два вида endpoint: query и mutation 

```jsx
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react' 

export const starWarsApi = createApi({ 
  reducerPath: 'starWars', 
  baseQuery: fetchBaseQuery({ baseUrl: "https://swapi.dev/api" }), 
  endpoints: (builder) => ({ 

    // Define endpoints here 
  }) 
}) 
```

Как было указано выше, существует два вида endpoint: `query` и `mutation`. Зададим два query endpoint’а:  

```jsx
endpoints: (builder) => ({ 
 getFilms: builder.query({ 
     query: () => `/films?format=json` 
  }), 

 getFilmById: builder.query({ 
   query: (filmId) => `/films/${filmId}?format=json` 
  }) 
}) 
```

В коде выше были добавлены два endpoint: 
1. _getFilms_. Получение списка всех фильмов; 
2. getFilmById. Получение одного фильма по его ID. В данном случае filmId представляет собой query параметр; при необходимости набор параметров можно расширить.  

*Самое интересное начинается здесь.*
Для каждого endpoint, объявленного выше, `RTK Query` автоматически генерирует хуки, которые могут быть использован в React компонентах для загрузки/изменения данных. Рассмотрим это на следующем примере: 

![](https://habrastorage.org/r/w1560/getpro/habr/upload_files/ff2/d32/48b/ff2d3248b5b2bd04764a6c71e3085f43.png)

Как видно на изображении, _starWarsApi_ после инициализации содержит в себе сгенерированные хуки. В зависимости от типов endpoint, название хуков будет содержать в себе либо _query_, либо _mutation_.  

Финальная версия Star Wars API Slice выглядит следующим образом:  

```jsx
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react' 

export const starWarsApi = createApi({ 
  reducerPath: 'starWars', 
  baseQuery: fetchBaseQuery({ baseUrl: "https://swapi.dev/api" }), 
  endpoints: (builder) => ({ 
    getFilms: builder.query({ 
      query: () => `/films?format=json` 
    }), 
    getFilmById: builder.query({ 
      query: (filmId) => `/films/${filmId}?format=json` 
    }) 
  }), 
}) 

export const { useGetFilmsQuery, useGetFilmByIdQuery } = starWarsApi 
 
```

Метод createApi генерирует `reducer`, который должен быть добавлен в `store`. Также для обеспечения возможностей `RTK Query` (кэширование, инвалидация, polling и др.) необходимо добавить `middleware` как на примере ниже:  

```jsx
import { configureStore } from '@reduxjs/toolkit' 
import { setupListeners } from '@reduxjs/toolkit/query' 
import { starWarsApi } from './services/starWarsApi' 

export const store = configureStore({ 
  reducer: { 
    // Add the generated reducer as a specific top-level slice 
    [starWarsApi.reducerPath]: starWarsApi.reducer, 
  }, 
  // Adding the api middleware enables caching, invalidation, polling, 
  // and other useful features of `rtk-query`. 
  middleware: (getDefaultMiddleware) => 
    getDefaultMiddleware().concat(starWarsApi.middleware), 
}) 

// optional, but required for refetchOnFocus/refetchOnReconnect behaviors 

// see `setupListeners` docs - takes an optional callback as the 2nd arg for customization 

setupListeners(store.dispatch) 
```

Настройка на этом завершена. Далее рассмотрим использование сгенерированных хуков в React компонентах.  

```jsx
import { useGetFilmsQuery } from '../reduxStore/services/starWarsApi'; 

const FilmsList = () => { 
  const { data, isLoading, error } = useGetFilmsQuery(); 

  return ( 
    <div> 
      <h3>Star Wars Movies</h3> 
      {error ? ( 
        <>Oh no, there was an error</> 
      ) : isLoading ? ( 
        <>Loading...</> 
      ) : data ? ( 
        <div> 
          {data.results.map(movie => ( 
            <section item key={movie.episode_id} xs={4}> 
              <h2>{movie.title}</h2> 
              <p>{movie.opening_crawl}</p> 
            </section> 
          ))} 
        </div> 
      ) : null} 
    </div> 
  ) 
} 

export default FilmsList; 
```

Рассмотрим описанный код выше: 
- Сначала мы просто импортировали хук _useGetFilmsQuery_ 
- При вызове хука useGetFilmsQuery будет автоматически производиться вызов к API для получения всех фильмов. Хук в свою очередь возвращает не только вышеуказанные значения, но и также ряд других полезных, таких как isFetching,  isError и другие. 

![](https://habrastorage.org/r/w1560/getpro/habr/upload_files/682/e4c/1cc/682e4c1cc3c01fc1fbe1421ec8a96405.png)

1. Теперь не приходится создавать `action creators` для каждого запроса 
2. Нет нужды создавать множество `reducers` 
3. Обработка состояний запросов (isFetching, isError и др.) теперь производится автоматически 
4. В React компонентах не нужно вызывать метод `dispatch` или использовать `селекторы` для взаимодействия со `store`  

В результате количество написанного кода становится меньше, а его восприятие заметно улучшилось.

##### Список источников

Подробнее:  [RTK query: что мы от него хотим и зачем](https://habr.com/ru/companies/alfa/articles/705640/) , [Как мы используем RTK Query в React-приложениях](https://habr.com/ru/companies/domrf/articles/736336/)

____
#React #redux #redux-toolkit #configureStore #RTK-Query

____

### [[004 React + Redux|Назад]]