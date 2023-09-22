```
//! Что будет в консоли?

const var1 = 5;

function tmp() {
    console.log(">>>>>>>>", var1);
}

function main() {
    const var1 = 10;
    tmp();
    console.log(var1);
}

main();
```