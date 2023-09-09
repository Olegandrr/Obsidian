![](https://www.youtube.com/watch?v=oh3Qa72pA3c&t=1s)

#### Ответ

Для работы со сложными структурами данных вам может потребоваться использовать такие методы, как сопоставление вложенных данных (маппинг, mapping), использование рекурсивных компонентов для визуализации данных с несколькими уровнями вложенности и оптимизация производительности с помощью таких методов, как `React.memo`. Также может быть полезно использовать библиотеки, такие как `lodash`, для управления и преобразования сложных структур данных. Например, функция `debounce` из библиотеки `lodash`, полезна для сокращения количества API запросов. 

Очевидно, что в React существует множество способов обработки сложных структур данных. Вот несколько сценариев, в которых вам, возможно, придется более осторожно подходить к обработке и представлению данных.
- Вложенные структуры данных, такие как дерево или граф.
- Большие наборы данных, которые необходимо отображать и обрабатывать в виде таблицы или списка.
- Структуры данных со многими уровнями вложенности, например, объект JSON с несколькими уровнями вложенных объектов и массивов.
- Структуры данных, которые постоянно меняются, например, данные в режиме реального времени из прямой трансляции или подключения через веб-сокет.

[Lo-Dash](http://lodash.com/) — это полноценная замена[*](https://github.com/bestiejs/lodash/wiki/Drop-in-Disclaimer) для [Underscore.js](http://underscorejs.org/). Lo-dash имеет более высокую производительность, избавлен от некоторых [багов](https://github.com/bestiejs/lodash#resolved-underscorejs-issues) underscore и даёт некоторые новые возможности.  
  
![](https://habrastorage.org/r/w1560/storage2/48f/3eb/821/48f3eb8216f7ecfe03af1b5418d2f3b3.png)

- Поддержка [AMD-загрузчиков](http://habrahabr.ru/post/152833/) ([RequireJS](http://requirejs.org/), [curl.js](https://github.com/cujojs/curl), etc.)
- [`_.clone`](http://lodash.com/docs#clone) поддерживает _“глубокое”_ клонирование
- [`_.forEach`](http://lodash.com/docs#forEach) поддерживает текучий интерфейс и остановку итерирования
- [`_.forIn`](http://lodash.com/docs#forIn) для итерирования по собственным и унаследованным свойствам объектов
- [`_.forOwn`](http://lodash.com/docs#forOwn) для итерирования только по собственным свойствам объекта
- [`_.isPlainObject`](http://lodash.com/docs#isPlainObject) проверяет, было ли значение создано с помощью конструктора `Object`
- [`_.lateBind`](http://lodash.com/docs#lateBind) для позднего связывания
- [`_.merge`](http://lodash.com/docs#merge) — _“глубокий”_ аналог [`_.extend`](http://lodash.com/docs#extend)
- [`_.partial`](http://lodash.com/docs#partial) для карринга без связывания `this`
- [`_.pick`](http://lodash.com/docs#pick) и [`_.omit`](http://lodash.com/docs#omit) принимают аргументы `callback` и `thisArg`
- [`_.template`](http://lodash.com/docs#template) использует [sourceURLs](http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/#toc-sourceurl) для более простой отладки
- [`_.contains`](http://lodash.com/docs#contains), [`_.size`](http://lodash.com/docs#size), [`_.toArray`](http://lodash.com/docs#toArray), [и т.д.…](http://lodash.com/docs "_.countBy, _.every, _.filter, _.find, _.forEach, _.groupBy, _.invoke, _.map, _.pluck, _.reduce, _.reduceRight, _.reject, _.shuffle, _.some, _.sortBy, _.where") принимают и строки тоже

Поддержка индивидуальных сборок позволяет легко создавать облегчённые версии `Lo-Dash`, содержащие только необходимые вам методы. Также `Lo-Dash` поддерживает за вас зависимости методов и псевдонимы.  
  
- Сборка, содержащая всё необходимое для работы [Backbone](http://backbonejs.org/), может быть создана с модификатором `backbone`.  
    ```
    lodash backbone
    ```
    
- [Content Security Policy](http://en.wikipedia.org/wiki/Content_Security_Policy) сборка.  
    ```
    lodash csp
    ```
    
- Сборка для старых браузеров без [поддержки ES5](http://es5.github.com/).  
    ```
    lodash legacy
    ```
    
- Сборки для мобильных платформ, без баг-фиксов для IE < 9 и компиляции методов.  
    ```
    lodash mobile
    ```
    
- Strict-сборки, с использованием [strict mode](http://es5.github.com/#C) для `_.bindAll`, `_.defaults`, and `_.extend`.  
    ```
    lodash strict
    ```
    
- Underscore-сборка, для тех, кто уже используется Underscore в своих проектах.  
    ```
    lodash underscore
    ```

- [Lo-Dash на Github](https://github.com/bestiejs/lodash/)
- [Установка Lo-Dash](http://lodash.com/#installation)
- [Документация API](http://lodash.com/docs)
- [Бенчмарки](http://lodash.com/benchmarks) + [еще бенчмарки на jsPerf.com](http://jsperf.com/search?q=lodash) _(в моём случае дают ускорение в 1.75 раз)_
- [Юнит-тесты](http://lodash.com/tests "Lo-Dash unit tests")

Подробнее: [Lo-Dash](https://habr.com/ru/companies/alawar/articles/157673/) , [Ссылка на методы Lodash](https://habr.com/ru/articles/217515/), [Хватит импортировать JavaScript-пакеты целиком](https://habr.com/ru/companies/ruvds/articles/502424/)

____
#React #HOC #Lodash #Debounce 

____

#### [[004 React + Redux|Назад]]