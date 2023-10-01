#### Ответ

#ESLint необходим для подсветки ошибок и работы с описанными правилами. 
#Prettier служит для чтения правил и форматирования кода .

-   eslint – главный модуль линтера.
-   eslint-config-airbnb  – готовая конфигурация для использования стайлгайда Airbnb.
-   eslint-config-prettier  – позволяет ESLint и Prettier работать вместе.
-   eslint-plugin-import – предназначен для поддержки синтаксиса импорта/экспорта и управления путями к файлам. Подробнее можно прочитать в [документации плагина](https://github.com/benmosher/eslint-plugin-import).
-   eslint-plugin-jsx-a11y 
-   eslint-plugin-react  – добавляет специфические настройки линтинга для проектов React.
-   eslint-plugin-react-hooks
-   husky _дает возможность зацепиться за хуки git. Это значит, что вы можете выполнять некоторые действия перед тем, как изменения будут закоммичены и отправлены в удаленный репозиторий_ .
-   lint-staged  _позволяет запускать тесты/форматеры на измененных файлах в pre-commit-хуке_

1.  `lint` - проверяет все файлы на ошибки
2.  `lint:fix` - проверяет и исправляет те ошибки, которые может
3.  `format` - форматирует все файлы с помощью prettier

Подробнее: [ESLint](https://habr.com/ru/companies/domclick/articles/743384/) , [Prettier](https://habr.com/ru/companies/ruvds/articles/428173/), [[000 Настройка eslint & prettier|Настройка eslint & prettier]] , [[002 Руководство Eslint + Prettier]]

____
#React #ESLint #Prettier 

____

#### [[004 React + Redux|Назад]]