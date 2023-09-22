```
// Написать функцию которая вернет наименьшее значение самого вложенного массива. 
/* 
Например из arr2 должно вернуться 100, так как самый вложенный массив содержит один элемент 100
const arr = [
    1,
    [
        [
            20, 
            1
        ],
        2
    ],
    [
        [
            -2
        ],
        [
            [
                100
            ]
        ]
    ]
]
*/

const arr2 = [1, [[20, 1], 2], [[-2], [[100]]]];

function findDeepestMinElement() {
}


console.log(findDeepestMinElement(arr2)); // [deepestLevelNumber, deepestMinElement]
```