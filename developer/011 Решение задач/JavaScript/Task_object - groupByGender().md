```
// Из исходного массива сделать объект, ключами которого будут все встречающиеся gender,
// а значениями массив объектов юзеров

const users = [
    {
        id: 1,
        name: "Виктория",
        gender: "female",
    },
    {
        id: 2,
        name: "Андрей",
        gender: "male",
    },
    {
        id: 3,
        name: "Александр",
        gender: "male",
    },
];

function groupByGender(users) {
    const groupedUsers = {};

    for (const user of users) {
        const { gender } = user;

        if (groupedUsers[gender]) {
            groupedUsers[gender].push(user);
        } else {
            groupedUsers[gender] = [user];
        }
    }

    return groupedUsers;
}

const groupedByGender = groupByGender(users);
console.log(groupedByGender);
```