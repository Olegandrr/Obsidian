function printContext() {
    console.log(this);
}

const printContextBind = printContext.bind({ a: 1 }).bind({ a: 2 });
printContextBind() // {a: 1}
printContextBind.call({a:3}) // {a: 1}
new printContextBind() // printContext{}

const myObj = {
    a: 10,
    method1() {
        const printThis = () => console.log(this);
        printThis();
    },
    method2: () => {
        const printThis = () => console.log(this);
        printThis();
    },
};

myObj.method1() // myObj
myObj.method2() // window

const res = myObj.method1.call({ a: 1 }) // {a: 1}
myObj.method2.call({a:1}) // window


const a = [0]
console.log(Boolean(a))