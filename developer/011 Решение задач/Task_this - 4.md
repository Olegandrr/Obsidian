// https://averom.notion.site/averom/JS-Review-86a9f74286484d68a01ccfffded67420

"useStrict"
var length = 4;

function cb() {
	console.log(this.length);
}

const object = {
	length: 5,
	method(cb) {
		cb();
	}
}

object.method(cb) // undefined
// console.log(object.method(cb))
