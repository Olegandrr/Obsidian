### Ответ

Для выполнения подобных проверок достаточно воспользоваться следующей конструкцией:

```ts
if (value) {
}
```

Выражение в скобках будет приведено к `true` в том случае, если оно не является чем-то из следующего списка:
- `null`
- `undefined`
- `NaN`
- Пустая строка
- 0
- `false`

TypeScript поддерживает те же правила преобразования типов, что и JavaScript.

___

tags: #TypeScript #null #undefined 

_____

### [[005 TypeScript|Назад]]