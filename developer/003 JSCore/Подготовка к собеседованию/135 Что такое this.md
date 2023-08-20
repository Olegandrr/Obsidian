![Что обозначает `this` в JavaScript?](https://youtu.be/rlWgI7AvV18?t=507)

#### Ответ

![[Pasted image 20230702192030.png|600]]

`this` - это ключевое слово, которое ссылается на объект, в контексте которого был вызван код. Значение `this` зависит от того, как был вызван код, и может изменяться в разных контекстах.

Значение `this` может быть определено в следующих контекстах:

1. В *глобальной области видимости*, `this` ссылается на объект `Window` в браузере или на объект `global` в Node.js.
    
2. В *методах объекта*, `this` ссылается на сам объект.
    
```javascript
const obj = {
  name: "John",
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

obj.greet(); // "Hello, my name is John"
```

3. В *функциях, вызванных с помощью методов объекта*, `this` ссылается на сам объект.
	
```javascript
const obj = {
  name: "John",
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

const myGreet = obj.greet;
myGreet(); // "Hello, my name is undefined"
```

4. В *конструкторах объектов*, `this` ссылается на новый экземпляр объекта, который создается при вызове конструктора.
	
```javascript
function Person(name) {
  this.name = name;
  this.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const john = new Person("John");
john.greet(); // "Hello, my name is John"
```

5. В *функциях, вызванных с помощью методов `call()`, `apply()` или `bind()`,* `this` ссылается на объект, переданный как первый аргумент.
	
```javascript
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

Значение `this` может быть сложным и зависит от контекста, поэтому важно понимать, как оно работает в разных ситуациях.

Подробнее: [[Контекст (this) в JS]] , [Ключевое слово this в JavaScript. Полное руководство](https://habr.com/ru/articles/464163/) , ![[Алгоритм использования ключевого слова `this`.canvas]]

___
 #JavaScript #object #this #call #apply #bind

___

### [[003 JSCore|Назад]]