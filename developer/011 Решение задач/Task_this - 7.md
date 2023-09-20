// Чему будет равен this в b1 и в b2 и почему ?
    
let a = {
    b1: function () {
        console.log(this);
    },
    b2: () => {
        console.log(this);
    },
};

a.b1();
a.b2();