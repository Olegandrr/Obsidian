____

tags: #TypeScript #union #type-guard 

[[005 TypeScript|На главную]]

1. Union типы и TypeGuards
![](https://www.youtube.com/watch?v=P2Ny05sAYoY)

2. Оператор ! (восклицательный знак) и пользовательские проверки типов
![](https://www.youtube.com/watch?v=bO1R4SnE8r8)


keywords:

#TypeGuard (охранник типа) - это механизм, который позволяет проверять типы значений во время выполнения программы и обеспечивает безопасность типов в TypeScript.

TypeGuard позволяет определять функции, которые могут проверять типы значений и возвращать булевое значение, указывающее, соответствует ли значение определенному типу. Если функция возвращает `true`, TypeScript рассматривает значение как соответствующее этому типу, и в дальнейшем можно использовать свойства и методы этого типа без ошибок компиляции.

Например, рассмотрим следующий код:

```typescript
function isString(value: any): value is string {
  return typeof value === "string";
}

let value: any = "hello";

if (isString(value)) {
  console.log(value.toUpperCase()); // Вывод: HELLO
} else {
  console.log("Value is not a string");
}
```

Здесь мы определяем функцию `isString`, которая проверяет, является ли значение типом `string`. Затем мы используем `isString` в условном операторе для проверки типа значения переменной `value`. Если `isString` возвращает `true`, мы можем безопасно использовать метод `toUpperCase` для строки `value`, так как TypeScript теперь рассматривает `value` как тип `string`.

TypeGuard в TypeScript может быть использован для обработки различных ситуаций, например, для проверки типа параметров функций, для проверки типа элементов массива или для проверки типа свойств объекта. Например:

```typescript
interface Person {
  name: string;
  age: number;
}

let obj: unknown = { name: "John", age: 30 };

function isPerson(value: any): value is Person {
  return typeof value === "object" && value !== null && "name" in value && "age" in value;
}

if (isPerson(obj)) {
  console.log(obj.name.toUpperCase()); // Вывод: JOHN
}
```

Здесь мы определяем интерфейс `Person` и переменную `obj`, которая содержит объект с полями `name` и `age`. Затем мы определяем функцию `isPerson`, которая проверяет, соответствует ли значение типу `Person`. В конце мы используем `isPerson` в условном операторе, чтобы проверить тип значения переменной `obj` и безопасно использовать свойство `name`.

_____

