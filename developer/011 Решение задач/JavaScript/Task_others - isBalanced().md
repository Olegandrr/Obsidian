```
function isBalanced(str) {

}

console.log(isBalanced("(x + y) - (4)")); // -> true
console.log(isBalanced("(((10 ) ()) ((?)(:)))")); // -> true
console.log(isBalanced("[({()})]")); // -> true
console.log(isBalanced("(50)((")); // -> false
console.log(isBalanced("[{]}")); // -> false
```