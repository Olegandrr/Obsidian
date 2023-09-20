// https://averom.notion.site/averom/JS-Review-86a9f74286484d68a01ccfffded67420
//! Что будет в консоли?

try {
	new Promise((res, rej) => {
		a++
		console.log(a);
		res(a);
	})
	.then(i => {
		console.log(i);
		a++;
		console.log(a);
		return a + i;
	})
	.catch((error) => {
		console.log(error)
		a++;
		return a;
	})
	.then((value) => console.log(value))
	.catch((error) => console.log(error));
	let a = 1;
	} catch (e) {
		console.log(e);
}