//! Что будет в консоли?

function createCounter() {
    let count = 0;

    let msg = `Count is ${count}`;

    const increase = () => (count += 1);
    const printMsg = () => console.log(msg);
    const printCount = () => console.log(count);

    return [increase, printMsg, printCount];
}
function runCreateCounter() {
    const [increase, printMsg, printCount] = createCounter();
    increase(); //
    increase(); //
    increase(); //
    printMsg(); // 
    printCount(); //
}

runCreateCounter()
