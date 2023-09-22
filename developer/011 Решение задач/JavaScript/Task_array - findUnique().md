```
//Написать метод массива, который будет возвращать массив уникальных значений 

// Array.prototype.findUnique = function() {

// };

// [10, 5, 10, 1, 6, 6, 6, 7, 9, 9, 10].findUnique();


// расширить массив методом findUnique, который возвращает новый массив, где перечислены только уникальные значения массива
[10, 5, 10, 6, 6, 7, 2, 9, 9, 'str', 'str', 'constructor', date, () => { }].findUnique(); // [5, 7, 2, date]

Array.prototype.findUnique = findUnique;
function findUnique() {

}

const obj = {}
console.log(obj.key); // undefined obj[key]
console.log(obj.constructor); // function
```