#JavaScript #array #reduce #taskJS 
___

```js
const foo = (arr) => {
// Ваш код
}

console.log(foo([1,1,1,2,2,2,2,4,4,5,0])) // [2,1,4,5,0]
```

### Ответ

```js
const foo = (arr) => {
	let res = [];

	const newObj = arr.reduce((acc, el) => {
		acc[el] ? acc[el]++ : (acc[el] = 1)
		return acc
	}, {});

	const sorted = Object.entries(newObj).sort((a, b) => b[1] - a[1]);

	for (let i = 0; i < sorted.length; i++) {
		res.push((Number(sorted[i][0])))
	}

	return res
}

console.log(foo([1,1,1,2,2,2,2,4,4,5,0])) // [2,1,4,5,0]
```

___
```js
	const newObj = arr.reduce((acc, el) => {
		acc[el] ? acc[el]++ : (acc[el] = 1)
		return acc
	}, {});

// Преобразование значения в виде
// {0: 1, 1: 3, 2: 4, 4: 2, 5: 1}
```