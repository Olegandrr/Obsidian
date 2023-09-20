```
/**
 * Функция должна преобразовывать строку в формат camelCase
 * @param str {string}
 */

const str = "mY-comPonent name";

function camelCase(str) {
    let convert = str.toLowerCase().replace('-', ' ').split(' ')
    let result = []
    for (let i = 0; i < convert.length; i++) {
        result += convert[i].charAt(0).toUpperCase() + convert[i].slice(1);
    }
    return result
}

console.log(camelCase("mY-comPonent name") === "MyComponentName");
console.log(camelCase(str))
```