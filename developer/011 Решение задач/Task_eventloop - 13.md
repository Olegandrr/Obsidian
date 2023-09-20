// // https://averom.notion.site/averom/JS-Review-86a9f74286484d68a01ccfffded67420
// //! Что будет в консоли?

// setTimeout(() => console.log(3), 2000);
// console.log(4);

// new Promise((res, rej) => {
// 	setTimeout(() => res());
// })
// .then(() => console.log(1))
// .catch(() => console.log(2));

// queueMicrotask(() => {
// 	console.log(5);
// 	queueMicrotask(() => {
// 		requestAnimationFrame(() => {
// 			console.log(8);
// 		});
// 		queueMicrotask(() => {
// 			console.log(7);
// 		});
// 	});
// });

// requestAnimationFrame(() => {
// 	console.log(3);
// 	requestAnimationFrame(() => {
// 		console.log(6);
// 	});
// });

// console.log(9);

// const obj = {
//   a: 1,
//   b: function() {
//     console.log(this.a)
//   },
//   c() {
//     console.log(this.a)
//   },
//   d: () => {
//     console.log(this.a)
//   },
//   e: (function() {
//     return () => {
//       console.log(this.a);
//     }
//   })(),
//   f: function() {
//     return () => {
//       console.log(this.a);
//     }
//   }
// }

// console.log(obj.a) //
// obj.b() //

// const b = obj.b
// b() //

// obj.b.apply({a: 2}) //

// obj.c() //

// obj.d() //

// obj.d.apply({a:2}) //

// obj.e()  //

// obj.e.call({a:2}) //

// obj.f()() //

// console.log(1);

// setTimeout(() => {
//     console.log(2);
// });

// requestAnimationFrame(() => {
//     console.log(6);
// });

// new Promise((res) => {
//     console.log(3);
//     res();
// }).then(() => {
//     console.log(5);
//     queueMicrotask(() => {
//         console.log(7);
//     });
// });
// console.log(4);



console.log(4);

new Promise((res, rej) => {
    setTimeout(() => res());
})
    .then(() => console.log(1))
    .catch(() => console.log(2));

queueMicrotask(() => {
    console.log(5);
    queueMicrotask(() => {
        requestAnimationFrame(() => {
            console.log(8);
        });
        queueMicrotask(() => {
            console.log(7);
        });
    });
});

requestAnimationFrame(() => {
    console.log(3);
    requestAnimationFrame(() => {
        console.log(6);
    });
});

console.log(9);


// var a = 10;

// function fn() {
//     if (1 == typeof 'number') {
//         return a
//     }
//     // return a;
// }
// console.log(fn());

//! Что будет в консоли?

// console.log(1)

// setTimeout(() => {
//     console.log(2);
// })

// requestAnimationFrame(() => {
//     console.log(6);
// })

// new Promise((res) => {
//     console.log(3);
//     res();
// }).

// then(() => {
//     console.log(5);
//     queueMicrotask(() => {
//         console.log(7)
//     })
// })
// console.log(4)

