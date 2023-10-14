![](https://www.youtube.com/watch?v=BTB3VDkWiOQ)
### Ответ

#Record Создает тип объекта, ключи свойств которого `Keys`, а значениями свойств - `Type`. 
Эту утилиту можно использовать для сопоставления свойств одного типа с другим типом.

```typescript
interface CatInfo {
	age: number;
	breed: string;
}

type CatName = "miffy" | "boris" | "mordred";

const cats: Record<CatName, CatInfo> = {
	miffy: { age: 10, breed: "Persian" },
	boris: { age: 5, breed: "Maine Coon" },
	mordred: { age: 16, breed: "British Shorthair" },
};
```

___
tags: #TypeScript #partial #required #nonnullable #record #readonly #readonlyArray

_____

### [[005 TypeScript|Назад]]