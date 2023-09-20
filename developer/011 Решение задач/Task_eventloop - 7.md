//! что будет в консоли, что выполнится

function task2() {
    const innerFunc1 = async () => console.log(1);
    const innerFunc2 = async () => {
        console.log(2);
        await innerFunc1();
        console.log(3);
    };
    innerFunc2();
    console.log(4);
}

task2();
