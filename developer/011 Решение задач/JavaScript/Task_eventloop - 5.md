//! что будет в консоли, что выполнится

Promise.resolve("a")
    .catch((v) => {
        throw v + "b";
    })
    .catch((v) => v + "c")
    .then((v) => v + "d")
    .then(() => console.log("e"));

console.log("f");
