### Ответ

#### Основные концепции

Вот некоторые основные функции и концепции Redux Toolkit:
- **[#configureStore](https://habr.com/ru/companies/inobitec/articles/481288/#configureStore)**— функция, предназначенная упростить процесс создания и настройки хранилища;
- **[#createReducer](https://habr.com/ru/companies/inobitec/articles/481288/#createReducer)**— функция, помогающая лаконично и понятно описать и создать редьюсер;
- **[#createAction](https://habr.com/ru/companies/inobitec/articles/481288/#createAction)**— возвращает функцию создателя действия для заданной строки типа действия;
- **[#createSlice](https://habr.com/ru/companies/inobitec/articles/481288/#createSlice)**— объединяет в себе функционал createAction и createReducer;
- **createSelector** — функция из библиотеки [Reselect](https://github.com/reduxjs/reselect), переэкспортированная для простоты использования.

*Redux Toolkit полностью интегрирован с TypeScript.* 
Более подробную информацию об этом можно получить из раздела [Usage With TypeScript](https://redux-toolkit.js.org/usage/usage-with-typescript/) официальной документации.

#### `configureStore()`

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

*Данный инструмент позволяет автоматически комбинировать редьюсеры, добавить мидлвары (по умолчанию включает redux-thunk), а также использовать расширение `Redux DevTools`. *

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

Для получения наиболее популярного списка мидлваров можно воспользоваться специальной функцией `getDefaultMiddleware`, также входящей в состав Redux Toolkit. Данная функция возвращает массив с включенными по умолчанию в библиотеку Redux Toolkit мидлварами. Перечень этих мидлваров отличается в зависимости от того, в каком режиме выполняется ваш код. *В production режиме массив состоит только из одного элемента — thunk.* В режиме development на момент написания статьи список пополняется следующими мидлварами:
- `serializableStateInvariant` — инструмент, специально разработанный для использования в Redux Toolkit и предназначенный для проверки дерева состояний на предмет наличия несериализуемых значений, таких как функции, Promise, Symbol и другие значения, не являющиеся простыми JS-данными;
- `immutableStateInvariant` — мидлвар из пакета [redux-immutable-state-invariant](https://www.npmjs.com/package/redux-immutable-state-invariant), предназначенный для обнаружения мутаций данных, содержащихся в хранилище.

#### `createReducer()`

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

##### Объединение `reducers` и последовательный их вызов

```jsx
import { createReducer } from '@reduxjs/toolkit';

// Редьюсер 1
const reducer1 = createReducer(initialState1, (builder) => {
  builder
    .addCase(actionType1, (state, action) => {
      // Обработка действия actionType1
    })
    .addCase(actionType2, (state, action) => {
      // Обработка действия actionType2
    });
});

// Редьюсер 2
const reducer2 = createReducer(initialState2, (builder) => {
  builder
    .addCase(actionType3, (state, action) => {
      // Обработка действия actionType3
    })
    .addCase(actionType4, (state, action) => {
      // Обработка действия actionType4
    });
});

// Объединение редьюсеров
const combinedReducer = createReducer(
  {},
  (builder) => {
    builder
      .addCase(actionType5, reducer1) // Вызов редьюсера 1 для действия actionType5
      .addCase(actionType6, reducer2); // Вызов редьюсера 2 для действия actionType6
  }
);
```

#### `createAction()`

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

#### `createSlice()`

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

#### Список источников

Подробнее: [Redux Toolkit](https://reactdev.ru/libs/redux-toolkit/#_46), [Redux Toolkit - официальная документация](https://redux-toolkit.js.org/) , [Redux Toolkit как средство эффективной Redux-разработки](https://habr.com/ru/companies/inobitec/articles/481288/) 
