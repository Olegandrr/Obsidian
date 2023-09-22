```
// Написать функцию чанк, которая принимает массив и какое кол-во элементов должно быть в чанке.
// Далее функция возвращает массив с массивами, как в комментах

const data = [1, 2, 3, 4, 5, 6, 7, 8, 9];

function chunk(arr, num) {
    let newArr = [];
    for (let i = 0; i < arr.length; i += num) {
        newArr.push(arr.slice(i, i + num));
    }
    return newArr;
}

console.log(chunk(data, 3)); // [[1,2,3],[4,5,6],[7,8,9]]
console.log(chunk(data, 4)); // [[1,2,3,4],[5,6,7,8],[9]]
console.log(chunk(data, 2)); // [[1,2],[3,4],[5,6],[7,8],[9]]

// console.log(chunk(data))
```