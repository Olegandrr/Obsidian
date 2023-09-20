```
// https://averom.notion.site/averom/JS-Review-86a9f74286484d68a01ccfffded67420

class First {
	constructor(type = "first") {
		this.type = type;
		this.init();
	}
	
	init() {
		console.log(this.type);
	}
}

class Second extends First {
	type = "second";
}
const first = new Second("foo"); //
const second = new Second(); //
second.init(); //
```