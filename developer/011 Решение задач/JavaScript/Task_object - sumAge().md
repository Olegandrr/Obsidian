```
function sumAge(user) {}

const user1 = {
    name: "Петр",
    age: 49,
    children: [
        {
            name: "Ника",
            age: 25,
            children: [
                {
                    name: "Андрей",
                    age: 3,
                },
                {
                    name: "Олег",
                    age: 1,
                },
            ],
        },
        {
            name: "Александр",
            age: 22,
        },
    ],
};

console.log(sumAge(user1)); // 100
```