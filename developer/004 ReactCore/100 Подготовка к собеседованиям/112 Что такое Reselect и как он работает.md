![Что такое Reselect и как он работает?](https://youtu.be/XtQPrt8G0n8?t=847)

#### Ответ

![[Pasted image 20230704193915.png|600]]

*Reselect* - это библиотека для работы с селекторами . 

*Селекторы* - это функции, которые позволяют получать данные из состояния приложения и преобразовывать их перед передачей в компоненты.

*Reselect* предоставляет удобный API для создания мемоизированных (memoized) селекторов, которые кэшируют результаты своих вычислений и пересчитывают их только тогда, когда их входные данные изменились.

Работа Reselect происходит следующим образом:
1. *Определение селекторов:* Создаются селекторы с помощью функции `createSelector()`, которая принимает входные данные и функцию-трансформер.
2. *Селекторы выполняются:* Когда компонент запрашивает данные из состояния приложения, селекторы выполняются и получают соответствующие данные из состояния.
3. *Результаты кэшируются:* Результаты вычислений сохраняются в кэше селектора.
4. *Проверка входных данных:* При следующем вызове селектора, его входные данные сравниваются с предыдущими значениями. Если данные не изменились, то результаты берутся из кэша, иначе селектор выполняется заново.
5. *Результаты возвращаются компоненту:* Результаты вычислений передаются в компоненты через свойства (props).

Это позволяет улучшить производительность приложения, уменьшив количество вычислений, которые выполняются повторно.

Вот пример создания мемоизированного селектора с помощью Reselect:

```jsx
import { createSelector } from 'reselect';

const getItems = state => state.items;
const getFilter = state => state.filter;

const getFilteredItems = createSelector(
  [getItems, getFilter],
  (items, filter) => {
    return items.filter(item => item.name.includes(filter));
  }
);

export default getFilteredItems;
```

В этом примере создается селектор getFilteredItems, который получает данные из состояния приложения (items и filter) и фильтрует их на основе значения filter. Селектор мемоизируется с помощью Reselect, что позволяет повторно использовать результаты вычислений, если входные данные не изменились.

Подробнее: [Несколько способов оптимизировать React-Redux приложение](https://habr.com/ru/articles/490526/)

____
#React #redux #reselect #selector 

____

#### [[004 React + Redux|Назад]]