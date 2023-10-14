#### Ответ

Значение `this` в JavaScript определяется во время выполнения кода, когда функция вызывается. Значение `this` зависит от контекста вызова функции, то есть от того, как именно была вызвана функция.

Значение `this` может быть определено в следующих контекстах:

1. В глобальной области видимости, `this` ссылается на объект `Window` в браузере или на объект `global` в Node.js.
	
```
console.log(this === window); // true (in a browser)
```

2. В методах объекта, `this` ссылается на сам объект.
	
```
const obj = {
  name: "John",
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

obj.greet(); // "Hello, my name is John"
```

3. В функциях, вызванных с помощью методов объекта, `this` ссылается на сам объект.
	
```
const obj = {
  name: "John",
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

const myGreet = obj.greet;
myGreet(); // "Hello, my name is undefined"
```

4. В конструкторах объектов, `this` ссылается на новый экземпляр объекта, который создается при вызове конструктора.
	
```
function Person(name) {
  this.name = name;
  this.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const john = new Person("John");
john.greet(); // "Hello, my name is John"
```

5. В функциях, вызванных с помощью методов `call()`, `apply()` или `bind()`, `this` ссылается на объект, переданный как первый аргумент.
	
```
const obj = {
  name: "John",
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

const otherObj = {
  name: "Jane"
};

obj.greet.call(otherObj); // "Hello, my name is Jane"
```

___
 #JavaScript #this #call #bind #apply

___

### [[003 JSCore|Назад]]