![Разница между внутренним (Internal Module) и внешним модулями (External Module)?](https://youtu.be/TOn-1RrowKE?t=807)

### Ответ

В TypeScript модули используются для организации кода и разделения его на отдельные файлы, что облегчает его повторное использование и поддержку. В TypeScript есть два типа модулей: внутренние ( #internal-modules ) и внешние модули ( #external-modules ).

## Внутренние модули #internal-modules 

Внутренние модули, также называемые пространствами имен (namespaces), позволяют группировать связанный код в одном месте. Они могут содержать классы, интерфейсы, функции и другие объекты и могут быть вложенными. Внутренние модули описываются с помощью ключевого слова `namespace`.

```tsx
namespace MyNamespace {
  export interface Person {
    name: string;
    age: number;
  }

  export function sayHello(person: Person) {
    console.log(`Hello, my name is ${person.name} and I am ${person.age} years old.`);
  }
}

const person: MyNamespace.Person = { name: 'John', age: 30 };
MyNamespace.sayHello(person); // Output: 'Hello, my name## Внешние модули (External Modules)
```

### Внешние модули #external-modules 

Внешние модули, также называемые модулями CommonJS или AMD, позволяют загружать код из отдельных файлов и использовать его в других проектах. Внешние модули могут импортировать и экспортировать объекты, функции, классы и другие элементы кода. 

Внешний модуль определяется в отдельном файле, который может быть загружен с помощью инструментов сборки, таких как Webpack или Rollup. Для экспорта элементов из модуля используется ключевое слово `export`, а для импорта элементов из других модулей используется ключевое слово `import`.

Вот пример определения и использования внешнего модуля:

```tsx
// myModule.ts
export interface Person {
  name: string;
  age: number;
}

export function sayHello(person: Person) {
  console.log(`Hello, my name is ${person.name} and I am ${person.age} years old.`);
}
```

```tsx
// app.ts
import { Person, sayHello } from './myModule';

constperson: Person = { name: 'John', age: 30 };
sayHello(person); // Output: 'Hello, my name is John and I am 30 years old.'
```

В этом примере мы определили внешний модуль `myModule`, который экспортирует интерфейс `Person` и функцию `sayHello()`. Затем мы импортировали эти элементы в файл `app.ts`, создали объект `person` типа `Person` и передали его в функцию `sayHello()`.

## Различия между внутренними и внешними модулями

Основное различие между внутренними и внешними модулями заключается в том, что *внутренние модули используются для организации кода в рамках одного проекта, а внешние модули используются для распространения кода между различными проектами и библиотеками.*

___
tags: #TypeScript #internal-modules #external-modules

_____

### [[005 TypeScript|Назад]]