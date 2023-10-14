### Ответ

Rest параметры позволяют передавать функции различное количество аргументов (ноль или более). Это полезно, когда вы не знаете, сколько параметров получит функция. Все аргументы после оставшегося символа `...` будут сохранены в массиве.

Например:

```typescript
function Greet(greeting: string, ...names: string[]) {
	return greeting + " " + names.join(", ") + "!";
}

Greet("Hello", "Steve", "Bill"); // returns "Hello Steve, Bill!"

Greet("Hello"); // returns "Hello !"
```

___
tags: #TypeScript #rest 

_____

### [[005 TypeScript|Назад]]