![Что такое `NaN`? Как определить, что значение равно `NaN`?](https://youtu.be/IooJ3P2VUYs?t=266)

#### Ответ

![[Pasted image 20230702121900.png|600]]

`NaN` - это специальное значение в JavaScript, которое означает "не число" (Not a Number). Это значение возвращается, когда математическая операция не может быть выполнена или когда результат не может быть представлен в виде числа. Например:

```javascript
const result = "hello" / 5;
console.log(result); // NaN
```

В этом примере, операция деления строки на число не может быть выполнена, поэтому результатом является `NaN`.

Чтобы проверить, что значение равно `NaN`, можно использовать функцию `isNaN()`. Однако, `isNaN()` не всегда работает так, как ожидается, потому что она пытается преобразовать аргумент в число, прежде чем проверить, является ли он `NaN`. Например:

```javascript
console.log(isNaN("hello")); // true
```

Это происходит потому, что `isNaN()` пытается преобразовать строку `"hello"` в число, что не удается, и возвращает `true`.

Более надежным способом проверки `NaN` является использование функции `Number.isNaN()`, которая возвращает `true`, только если аргумент является `NaN`. Например:

```javascript
console.log(Number.isNaN("hello")); // false
console.log(Number.isNaN(NaN)); // true
```

В этом примере, `Number.isNaN()` возвращает `false` для строки `"hello"`, потому что строка не является `NaN`, и `true` для `NaN`, потому что это действительно `NaN`.

___
#JavaScript #NaN

___

### [[003 JSCore|Назад]]