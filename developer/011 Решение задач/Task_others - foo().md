tags:  #JavaScript
___

```js
// Нужно написать функцию, которая соберет из полей `value` строку. Она должна формироваться по принципу:

// 1. Каждая строка должна быть развернута
// 2. Нужны только записи с `expired: false`
// 3. Записи должны быть отсортированы в порядке `order`
// 4. Если буква уже была использована, то ее не нужно добавлять

// Тут нужно еще было пояснить почему я делал именно так как сделал, а не по другому

const input = [
    { value: "qweq", order: 4, expired: false },
    { value: "asdq", order: 2, expired: true },
    { value: "jkri", order: 1, expired: false },
    { value: "oiod", order: 3, expired: false },
];

function foo(input) {

}

const result2 = "jkriodqwe"; // Нужно получить это

console.log(foo(input));
console.log(foo(input) === result2);
```

### Ответ
```js

```

___
### [[011 Решение задач JS, TS и React|Назад]]