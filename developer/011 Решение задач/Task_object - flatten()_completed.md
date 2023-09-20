tags: #JavaScript #flat #taskJS 
____

```js
function flatten(array) {
// Ваш код здесь
}

console.log(flatten([[1], [[2, 3]], [[[[[4]]]]]])); // -> [1, 2, 3, 4]
```

### Ответ

```js
const arr = [[1], [[2, 3]], [[[4]]]]

function flatten(arr) {
	return arr.flat(Infinity)
}

console.log(flatten(arr)); // -> [1, 2, 3, 4]
```