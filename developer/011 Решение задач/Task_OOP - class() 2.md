```
// https://averom.notion.site/averom/JS-Review-86a9f74286484d68a01ccfffded67420

var animal = { jumps: null };
var rabbit = { jumps: true };

rabbit.__proto__ = animal;

console.log( rabbit.jumps ); //

delete rabbit.jumps;
console.log( rabbit.jumps ); //

delete animal.jumps;
console.log( rabbit.jumps); //
```