![Для чего применяется метод `Array.from()`?](https://youtu.be/lZNWrW39ELM?t=328)

#### Ответ

![[Pasted image 20230702145750.png|600]]

Метод `Array.from()` в JavaScript используется для создания нового массива из итерируемого или массивоподобного объекта, то есть объекта, который имеет свойство `length` и элементы, доступные по индексу. Этот метод принимает один обязательный аргумент - итерируемый или массивоподобный объект - и необязательный второй аргумент - функцию-маппер, которая может быть использована для манипуляции с каждым элементом в процессе создания нового массива. Формат метода: `Array.from(arrayLike[, mapFn[, thisArg]])`.

Пример использования метода `Array.from()` для создания нового массива из строки:

```javascript
const str = 'hello';
const arr = Array.from(str);
console.log(arr); // ['h', 'e', 'l', 'l', 'o']
```

Пример использования метода `Array.from()` с функцией-маппером:

```javascript
const arr = [1, 2, 3];
const mappedArr = Array.from(arr, function(item) {
  return item * 2;
});
console.log(mappedArr); // [2, 4, 6]
```

Метод `Array.from()` можно использовать для создания новых массивов из других итерируемых объектов, таких как `Set`, `Map` и `arguments`, а также для создания массивов из объектов, которые не являются итерируемыми, но имеют свойство `length` и доступные по индексу элементы.

Одно из применений метода `Array.from()` - это создание копии массива, так как он создает новый массив, а не изменяет существующий. Кроме того, метод `Array.from()` может быть использован для преобразования других коллекций в массивы, чтобы облегчить их дальнейшую обработку.

___
#JavaScript #array #arrayFrom 

___

### [[003 JSCore|Назад]]