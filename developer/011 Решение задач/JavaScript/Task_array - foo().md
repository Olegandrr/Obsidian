```
//изменить код так, что бы в итоге выводился массив i ([], [1], [1, 1]) (сейчас выводится [1, 1, 1])

function foo() {
    for (let i = []; i.length < 3; i.push(1)) {
        setTimeout(console.log(i), i.length * 1000)
    }
}

console.log(foo())
```