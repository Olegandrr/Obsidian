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

a.sayName() 
// Bill

var b = a.sayName()

// b()
// b is not a function

a.sayName.bind({ firstName: 'Boris' })();
// Boris

a.sayName()
// Bill

a.sayLastName()
// undefined

a.sayName.bind({ firstName: 'Boris' }).bind({ firstName: 'Tom' })()
// Boris

a.sayLastName.bind({ lastName: 'Petrov' })()
// undefined
