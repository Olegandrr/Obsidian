```
/* Задача 3:
Дана структура данных в виде дерева
Необходимо написать функцию, возвращающую значения всех вершин дерева:
getTreeValues(tree); // => [1, 2, 3, 4, 5, 6, 7]
*/

const tree = {
    value: 1,
    children: [
        {
            value: 2,
            children: [{ value: 4 }, { value: 5 }],
        },
        {
            value: 3,
            children: [{ value: 6 }, { value: 7 }],
        },
    ],
};

const getRes = (obj) => {

    // return obj.children[0].children[0].value
};

console.log(getRes(tree));
```
