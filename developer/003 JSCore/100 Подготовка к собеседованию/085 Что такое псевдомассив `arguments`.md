![Что такое псевдомассив `arguments`?](https://youtu.be/kx3dR6ztICU?t=442)

#### Ответ

![[Pasted image 20230702150039.png|600]]

`arguments` - это псевдомассив, доступный внутри функции в JavaScript, который содержит значения всех аргументов, переданных в функцию, а также имеет свойство `length`, содержащее количество переданных аргументов.

Псевдомассив `arguments` имеет набор методов, которые обычно доступны для массивов, таких как `length`, `push()`, `pop()`, `slice()` и т.д. Однако, `arguments` не является полноценным массивом, так как у него нет всех методов и свойств, которые есть у настоящего массива, таких как `forEach()`, `map()`, `filter()`, `reduce()` и т.д.

Пример использования псевдомассива `arguments`:

```javascript
function sum() {
  let result = 0;
  for (let i = 0; i < arguments.length; i++) {
    result += arguments[i];
  }
  return result;
}

console.log(sum(1, 2, 3)); // 6
console.log(sum(4, 5, 6, 7)); // 22
```

В этом примере функция `sum()` принимает любое количество аргументов и использует псевдомассив `arguments` для вычисления их суммы.

Хотя псевдомассив `arguments` может быть полезен в некоторых случаях, его использование может привести к необходимости написания дополнительного кода для обработки аргументов функции, а также может сделать код менее читабельным. Поэтому в новом коде рекомендуется использовать синтаксис `rest` и `spread` для работы с переменным числом аргументов функции, а не использовать псевдомассив `arguments`.

___
#JavaScript #arguments

___

### [[003 JSCore|Назад]]