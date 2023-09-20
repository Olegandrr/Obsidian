//! будет ли обработан ответ?
/*
fetch('http://www.speedtest.net')
    .then(function (response) {
        console.log(response);
    })
    .catch(function (error) {
        console.error(error);
    });
while (true) console.log(1);
*/
 // нет


//! task
//! Что будет в консоли?

setTimeout(() => console.log(1));

function run() {
    return Promise.resolve(10).then(() => run());
}

run();

console.log(2);
//  // также нет 

