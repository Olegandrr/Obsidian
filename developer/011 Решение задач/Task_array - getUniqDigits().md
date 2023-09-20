```
// вернуть массив уникальных чисел

const arr = ['a',0,4,'4','0',5,'d',7,0,'8',7,10,'s',1,3,'9',10,3,1,9,'u',6,5,'2'];

const getUniqDigits = (arr) => {
    const changed = new Set(
        arr
            .map((el) => Number(el))
            .filter((el) => {
                return Number(el);
            })
            .sort((a, b) => a - b)
    );

    return [...changed];
};

console.log(getUniqDigits(arr)); // output [0,1,2,3,4,5,6,7,8,9,10]`
```