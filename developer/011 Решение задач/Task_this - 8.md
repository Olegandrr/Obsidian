// "useStrict
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

a.sayName() //

var b = a.sayName()

// b() //

a.sayName.bind({firstName: 'Boris'})(); // 

a.sayName() // 
a.sayLastName() // 

a.sayName.bind({firstName: 'Boris'}).bind({firstName: 'Tom'})() // 

a.sayLastName.bind({lastName: 'Petrov'})() // 