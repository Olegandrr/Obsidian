// https://averom.notion.site/averom/JS-Review-86a9f74286484d68a01ccfffded67420
//! Что будет в консоли?

console.log(1)

setTimeout(() => {
	console.log(2);
})

requestAnimationFrame(() => {
	console.log(6);
})

new Promise((res) => {
	console.log(3);
	res();
}).
then(() => {
	console.log(5);
	queueMicrotask(() => {
		console.log(7)
	})
})

console.log(4)