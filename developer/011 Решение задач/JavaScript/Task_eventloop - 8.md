// // ! Что будет в консоли после выполнения кода?

// var x = 3;

// var obj = {
//  x: 2,
//  foo: {
//    x: 1,
//    bar: function () {
//      console.log(this.x);
//    },
//    baz: function () {
//      setTimeout(function () {
//        console.log(this.x);
//      });
//    }
//  }
// };

// obj.foo.bar();
// var func = obj.foo.bar
// func();
// obj.foo.baz();
// x = 4;

//

const object = {
    message: "Hello, World!",
    logMessage() {
        console.log(this.message); // What is logged?
    },
};

setTimeout(object.logMessage(), 1000);       