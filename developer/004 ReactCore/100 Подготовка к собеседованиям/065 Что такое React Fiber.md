![Что такое React Fiber?](https://youtu.be/RpcB5jnJvcI?t=689)

![](https://www.youtube.com/watch?v=ZCuYPiUIONs)
#### Ответ

![[Pasted image 20230704195043.png|600]]

##### Введение

*Fiber* был введен в React начиная с версии 16 в 2017 году. Он позволил увеличить FPS отображения элементов на экране до 60 кадров в секунду.

*Fiber* - это переработанный и улучшенный алгоритм согласования *(`reconciliation`)* компонентов и обновления DOM-дерева, который разбивает работу на мелкие части (фибры-волокна) в виде дерева односвязного списка, они могут быть приостановлены и возобновлены по мере необходимости. 

##### Цель

*Основная цель React Fiber* - это улучшение производительности React-приложений путем уменьшения времени блокировки главного потока выполнения JavaScript (JavaScript main thread). *Это означает, что React может перераспределять ресурсы процессора между фибрами и использовать дополнительные потоки выполнения для выполнения тяжелых задач.*

##### `Concurrent Mode`

###### Что такое `Concurrent Mode` ?

`Concurrent Mode` - это новая функциональность в библиотеке React, которая была представлена в React начиная с версии 16.6.0. Это означает, что эта функциональность доступна разработчикам с октября 2018 года. Однако, следует отметить, что `Concurrent Mode` все еще находится в активной разработке и может быть изменен или дополнен в будущих версиях React.

`Concurrent Mode` позволяет React выполнять работу по приоритетам, что позволяет приложениям оставаться отзывчивыми и отображать актуальное состояние, даже если есть много работы, которую нужно выполнить. Он позволяет React эффективно распределять ресурсы и обрабатывать обновления компонентов без блокировки пользовательского интерфейса.

1. **Приоритеты**: определяет приоритеты работы и  позволяет выполнять задачи в соответствии с этими приоритетами. Это позволяет приложениям оставаться отзывчивыми и предоставлять лучший пользовательский опыт.
2. **Приостановка и возобновление**: позволяет приостанавливать выполнение работы, если она не является необходимой для отображения актуального состояния пользовательского интерфейса. Это позволяет более эффективно использовать ресурсы и улучшает производительность приложений.
3. **Отмена**: `Concurrent Mode` позволяет React отменять работу, которая была запланирована, но больше не требуется. Это особенно полезно для обработки пользовательских действий, которые могут быть отменены или заменены другими действиями.

###### Как переключить проект в `Concurrent Mode` ?

**Конкурентный режим**— это именно режим, поэтому его потребуется включить. Как тумблер, который заставляет Fiber работать на полную мощность. С чего же начать?  
  
Убираем легаси. Избавляемся от всех устаревших методов в коде и убеждаемся, что их нет в библиотеках. Если приложение без проблем работает в React.StrictMode, то всё в порядке — переезд будет простым. Потенциальная сложность — проблемы внутри библиотек. В этом случае нужно либо перейти на новую версию, либо сменить библиотеку. Или же отказаться от конкурентного режима. После избавления от легаси останется только переключить root.  
  
С приходом Concurrent Mode будет доступно три режима подключения root:  
  
- **Старый режим**  
    `ReactDOM.render(<App />, rootNode)`  
    Рендер после выхода конкурентного режима устареет.
    
- **Блокирующий режим**  
    `ReactDOM.createBlockingRoot(rootNode).render(<App />)`  
    В качестве промежуточного этапа будет добавлен блокирующий режим, который даёт доступ к части возможностей конкурентного режима на проектах, где есть легаси или другие трудности с переездом.
    
- **Конкурентный режим**  
    `ReactDOM.createRoot(rootNode).render(<App />)`  
    Если всё хорошо, нет легаси, и проект можно сразу переключить, замените в проекте рендер на createRoot — и вперёд в светлое будущее.
###### Список источников

Подробнее: [`Concurrent Mode`](https://reactjs.org/docs/concurrent-mode-intro.html) , [React 18](https://react.dev/blog/2022/03/08/react-18-upgrade-guide) , [Concurrent Mode в React: адаптируем веб-приложения под устройства и скорость интернета](https://habr.com/ru/companies/yandex/articles/514016/comments/) ,  [[025 Что такое «ленивая» (Lazy) функция|Что такое `<Suspense/>`]]

##### Планировщик задач

*Фибры разбиваются и выполняются по приоритету выполнения. Регулирует приоритетность выполнения работ - планировщик Fiber.* Ниже приведены различные типы работ, упорядоченные по приоритету от самого высокого к самому низкому: 

1. **Анимация (Animation)**.
2. **Synchronous (Sync)**: *Это самый высокий приоритет. Работы синхронного типа выполняются немедленно, не ожидая прерывания или приостановки.
3. **Task**: Работы типа Task имеют ниже приоритет, чем синхронные работы. *Они представляют асинхронные задачи, такие как обработка сетевых запросов (AJAX), выполнение таймеров или других асинхронных операций.*
4. **High Priority**: Работы с высоким приоритетом имеют более высокий приоритет, чем работы низкого приоритета, и выполняются после завершения задач и синхронных работ. *Этот тип работы может использоваться для обработки важных событий или изменений данных, которые должны быть обновлены немедленно, но не критичны для отзывчивости пользовательского интерфейса.*
5. **Normal Priority**: Работы типа Normal Priority выполняются после всех задач, синхронных работ и работ с высоким приоритетом. *Они представляют типичные задачи перерисовки компонентов и обновления состояния.* Большинство обычных операций React выполняются с помощью работ нормального приоритета.
6. **Low Priority**: Работы с низким приоритетом имеют наименьший приоритет и выполняются после всех других работ. *Они обычно используются для задач, которые не требуют мгновенной обработки и могут быть отложены до более подходящего момента.* Например, загрузка данных с сервера, предварительное вычисление или другие несрочные операции могут быть запланированы как работы с низким приоритетом.

##### Список источников

Подробнее: 
* [React Fiber](https://habr.com/ru/articles/444276/) , 
* [Что такое React Fiber](https://dev.to/jennypollard/chto-takoie-react-fiber-react-fiber-architecture-2cho), 
* [React Fiber. Все только начинается](https://www.youtube.com/watch?v=TYEIovD-llI),
* [Fiber изнутри: Погружение в новый алгоритм согласования React](https://habr.com/ru/articles/662549/), 
* [Как React 18 улучшает производительность приложения](https://my-js.org/blog/react-18/), 
* [Как длительные задачи JavaScript повышают время Time to Interactive](https://web.dev/long-tasks-devtools/#what-are-long-tasks) , 


____
#React #fiber #reconciliation #VirtualDOM 

____

#### [[004 React + Redux|Назад]]