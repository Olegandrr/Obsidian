// "use strict";

const obj1 = {
    name: "Alice",
    func1() {
        return function () {
            console.log(this.name);
        };
    },
};

const obj2 = {
    name: "Bob",
    func2: obj1.func1(),
};

const func = obj2.func2;

func(); // undefined
obj2.func2() // Bob
