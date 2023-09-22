//! что будет в консоли, что выполнится

[1, 2].forEach((i) => console.log(i));
setTimeout(() => console.log(3));
new Promise((resolve) => {
    console.log(4);
    resolve(5);
}).then((i) => console.log(i));
console.log(6);
