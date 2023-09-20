```
//ЕСТЬ СТРУКТУРА ДАННЫХ

const structure = [
  "a.js",
  "b.js",
  {
    src: [
      "some.js",
      "other.js",
      {
        components: [
          "someComponent.js",
          {
            input: ["input.js"],
          },
        ],
      },
    ],
  },
];

/*
ФУНКЦИЯ ДОЛЖНА ВЕРНУТЬ 

[
  'a.js',
  'b.js',
  'src/some.js',
  'src/other.js',
  'src/components/someComponent.js'
]
*/

// РЕШЕНИЕ

const flutter = (arr, divider = "") => {

};
```