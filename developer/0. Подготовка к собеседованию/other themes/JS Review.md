
* [[102 Что такое ECMAScript|Что такое ECMAScript? В чём отличие от JavaScript?]]
* [[040 Какие есть типы данных в JavaScript|Какие есть типы данных в JavaScript?]]
* [[086 Что такое область видимости|Что такое область видимости `(scope)` ?]]

* [[089 Что такое лексическое окружение. Что такое замыкание|Что такое лексическое окружение? Что такое замыкание?]]
* [[107 Что такое деструктуризация|Что такое деструктуризация?]]
* [[142 Что такое цепочка вызовов функций (chaining). Как реализовать такой подход|Что такое цепочка вызовов функций (chaining)? Как реализовать такой подход?]]

```javascript
//Что будет выводится в консоль?

function createCounter() {
    let count = 0;
    let msg = `Count is ${count}`;
    
    const increase = () => (count += 1);
    const printMsg = () => console.log(msg);
    const printCount = () => console.log(count);

    return [increase, printMsg, printCount];
}

function runCreateCounter() {
    const [increase, printMsg, printCount] = createCounter();

    increase(); 
    increase(); 
    increase(); 

    printMsg(); //
    printCount(); //
}

runCreateCounter()
```

```
Первая строка вывода `Count is 0` является результатом вызова функции `printMsg()`, которая выводит сообщение, содержащее текущее значение `count` в момент создания замыкания (которое равно 0).

Вторая строка вывода `3` является результатом вызова функции `printCount()`, которая выводит текущее значение переменной `count` (которое было увеличено три раза с помощью функции `increase()`).
```

* [[103 В чём разница между var, let и const|В чём разница между var, let и const?]]
* [[093 Что такое всплытие hoisting|Что такое всплытие `hoisting`?]]
* [[104 Что такое временная мёртвая зона (temporal dead zone)|Что такое временная мёртвая зона (temporal dead zone)?]]

```javascript
//Что будет выводится в консоль?
let b = 5;

function foo(a = b, b) {
    console.log(a, b) //
}

foo(undefined, 2) //
```

* [[096 Что означает функции высшего порядка|Что означает функции высшего порядка?]]
* [[101 Что делает reduce. Какие аргументы принимает|Что делает `reduce`? Какие аргументы принимает?]]
* [[095 Плюсы и минусы иммутабельности|Плюсы и минусы иммутабельности? Как достичь иммутабельности в JS?]]
* [[174 Для чего используются метод `Object.seal()`|Для чего используются метод `Object.seal()`?]]
* [[175 Разница между `Object.freeze()` и `Object.seal()`|Разница между `Object.freeze()` и `Object.seal()`?]]
* [[105 Можно ли изменить значение определённое через `const`|Можно ли изменить значение определённое через `const`?]]

* [[135 Что такое this|Что такое `this`?]]
* [[139 Что такое потеря контекста|Что такое потеря контекста?]]

```javascript
const obj = {
  a: 1,
  b: function() {
    console.log(this.a)
  },
  c() {
    console.log(this.a)
  },
  d: () => {
    console.log(this.a)
  },
  e: (function() {
    return () => {
      console.log(this.a);
    }
  })(),
  f: function() {
    return () => {
      console.log(this.a);
    }
  }
}

console.log(obj.a) // 
obj.b() // 

const b = obj.b 
b() // 

obj.b.apply({a: 2}) // 

obj.c() // 

obj.d() // 

obj.d.apply({a:2}) // 

obj.e()  // 

obj.e.call({a:2}) // 

obj.f()() // 

```


```javascript
function printContext() {
    console.log(this);
}

const printContextBind = printContext.bind({ a: 1 }).bind({ a: 2 });

printContextBind() // 

printContextBind.call({a:3}) // 

new printContextBind() //

const myObj = {
    a: 10,
    method1() {
        const printThis = () => console.log(this);
        printThis();
    },
    method2: () => {
        const printThis = () => console.log(this);
        printThis();
    },
};

myObj.method1() // 

myObj.method2() // 

const res = myObj.method1.call({ a: 1 }) //

myObj.method2.call({a:1}) // 

```

* [[185 Как работает instanceof|Как работает `instanceof`?]]
* [[186 Разница между `typeof` и `instanceof`|Разница между `typeof` и `instanceof`?]]
* [[177 Что такое класс и для чего он нужен|Что такое класс и для чего он нужен?]]

* [[001 Что такое DOM|Что такое DOM?]]
* [[008 Виды событий в JavaScript|Виды событий в JavaScript?]]
* [[023 Разница между событиями `load` и `DOMContentLoaded`|Разница между событиями `load` и `DOMContentLoaded`?]]
* [[010 Как добавить обработчик события на DOM-элемент|Как добавить обработчик события на DOM-элемент?]]
* [[011 Сколько аргументов принимает `addEventListener`|Сколько аргументов принимает `addEventListener`?]]

* [[201 Что такое Eventloop, очередь задач, микрозадача и макрозадача|Что такое `Eventloop`, очередь задач, микрозадача и макрозадача?]]
* [[203 Подходы при работе с асинхронным кодом|Подходы при работе с асинхронным кодом?]]
* [[199 Многопоточность против асинхронного программирования|Многопоточность против асинхронного программирования?]]
* [[210 Как обрабатывать ошибки в промисах|Как обрабатывать ошибки в промисах?]]

```javascript
//! Что будет в консоли?

console.log(1)

setTimeout(() => {
    console.log(2);
})

requestAnimationFrame(() => {
    console.log(6);
})

new Promise((res) => {
    console.log(3);
    res();
}).

then(() => {
    console.log(5);
    queueMicrotask(() => {
        console.log(7)
    })
})
console.log(4)
```

```javascript
//! Что будет в консоли?

setTimeout(() => console.log(3), 2000);

console.log(4);

new Promise((res, rej) => {
    setTimeout(() => res());
})
.then(() => console.log(1))
.catch(() => console.log(2));

queueMicrotask(() => {
    console.log(5);
    queueMicrotask(() => {
        requestAnimationFrame(() => {
            console.log(8);
        });
        queueMicrotask(() => {
            console.log(7);
        });
    });
});

requestAnimationFrame(() => {
    console.log(3);
    requestAnimationFrame(() => {
        console.log(6);
    });
});

console.log(9);
```
