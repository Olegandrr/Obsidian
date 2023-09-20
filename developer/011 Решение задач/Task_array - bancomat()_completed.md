#JavaScript #array #taskJS 
___
```js
const bancomat = (money) => {
// Ваш код здесь
}; 

//доступные купюры 100, 50, 20, 10 

console.log(bancomat(280)); // [100, 100, 50, 20, 10]
```

### Ответ

```js
const bancomat = (money) => {
	const available = [100, 50, 20, 10]; //доступные купюры 100, 50, 20, 10
	let lastMoney = []

	for (let i = 0; i < available.length; i++) {
		let note = available[i]
		
		while(money >= note) {
			lastMoney.push(note);
			money -= note;
		}
	}

	return lastMoney
};

console.log(bancomat(280)); // [100, 100, 50, 20, 10]
```