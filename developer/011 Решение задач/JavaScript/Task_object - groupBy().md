```
// Сегодня на собесе попалась задачка на парсинг даты, может кому пригодится:
// Вызов функции - groupBy(persons, "age") 

const persons = [
  { name: 'Alex', age: 20 },
  { name: 'Lena', age: 25 },
  { name: 'Pavel', age: 20 }
]

function groupBy(arr, prop) {
    // let map = new Map(arr, prop)
    // return JSON.parse(prop.age, arr)
    console.log(arr[prop])
}


console.log(groupBy(persons, 'age'))

// Результат {
//   20: [{ name: 'Alex', age: 20 }, { name: 'Pavel', age: 20 } ],
//   25: [{ name: 'Lena', age: 25 }]
// }
```
