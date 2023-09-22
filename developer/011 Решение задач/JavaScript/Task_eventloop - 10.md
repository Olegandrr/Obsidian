// https://averom.notion.site/averom/JS-Review-86a9f74286484d68a01ccfffded67420
//! Что будет в консоли?

// const a = setTimeout(() => console.log(2), 2000);
// const d = setTimeout(() => console.log(6), 1000);

// const c = new Promise( (resolve) => {
//    setTimeout(() => resolve(), 1000);
//    console.log(4);
// });
// c.then(() => console.log(1));

// const b = setTimeout(() => console.log(5), 1000);

// console.log(3);

var a = {
	firstName: 'Bill',
	lastName: 'Ivanov',
	sayName: function() {
		console.log(this.firstName)
	},
	sayLastName: () => {
		console.log(this.lastName)
	}
};

a.sayName() //Bill

var b = a.sayName()

// b() // undefined

a.sayName.bind({firstName: 'Boris'})(); // Boris

a.sayName() // Bill
a.sayLastName() // undefined

a.sayName.bind({firstName: 'Boris'}).bind({firstName: 'Tom'})() // Boris

a.sayLastName.bind({lastName: 'Petrov'})() // undefined
