const firstPromise = new Promise((resolve, reject) => {
    setTimeout(resolve, 500, "один");
});

const secondPromise = new Promise((resolve, reject) => {
    setTimeout(reject, 100, "два");
});

Promise.all([firstPromise, secondPromise])
    .then((res) => console.log(res))
    .catch((err) => console.log(err)); //два
Promise.allSettled([firstPromise, secondPromise])
    .then((res) => console.log(res))
    .catch((err) => console.log(err)); // один, два
Promise.any([firstPromise, secondPromise])
    .then((res) => console.log(res))
    .catch((err) => console.log(err)); // один
Promise.race([firstPromise, secondPromise])
    .then((res) => console.log(res))
    .catch((err) => console.log(err)); // два
