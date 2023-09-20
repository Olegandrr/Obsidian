var a = {
    firstName: "Bill",
    lastName: "Ivan",
    sayName: function () {
        console.log(this.firstName);
    },
    sayLastName: (arg) => {
        console.log(this.lastName, arg);
    },
};

a.sayName(); // Bill

var b = a.sayName;
b(); // window

a.sayName.bind({ firstName: "Boris" })(); // Boris
a.sayName(); // Bill
a.sayLastName(); // und
a.sayName.bind({ firstName: "Boris" }).bind({ firstName: "Tom" })(); // Bind
a.sayLastName.bind({ lastName: "Jim" }, 2)(); // und 2
