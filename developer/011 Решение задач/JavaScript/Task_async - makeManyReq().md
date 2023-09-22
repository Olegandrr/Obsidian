```
// Дан список ссылок и функция запроса
// Необходимо реальзовать процедуру запроса всех сылок из списка

function makeManyReq() {
    const urls = ["https://yandex.ru", "https://mail.ru", "https://rambler.ru"];

    function fetchUrl(url) {
        return Promise.resolve(`Succses ${url}`);
    }

    const promisesArr = urls.map((url) => fetchUrl(url));
    const answer = Promise.all(promisesArr);

    // если одна ссылка выполнится с ошибкой то вернется ошибка,
    // тогда нужно использовать allSettled

    answer.then((res) => console.log(res));
}
```