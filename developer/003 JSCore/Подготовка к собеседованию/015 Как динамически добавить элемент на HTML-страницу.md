![Как динамически добавить элемент на HTML-страницу?](https://youtu.be/nvktMVFM0_M?t=551)

#### Ответ

![[Pasted image 20230701215800.png|600]]

Для того чтобы динамически добавить элемент на HTML-страницу в JavaScript, можно использовать функцию `createElement()`, чтобы создать новый элемент, а затем добавить его на страницу с помощью метода `appendChild()` или `insertBefore()`.

Вот пример использования функции `createElement()` для создания нового элемента `div`, и метода `appendChild()` для добавления его в конец родительского элемента:

```javascript
const parentElement = document.getElementById('parent');
const newDiv = document.createElement('div');
newDiv.innerHTML = 'Новый элемент';
parentElement.appendChild(newDiv);
```

В этом примере мы используем метод `getElementById()` для получения родительского элемента по его идентификатору, затем используем функцию `createElement()` для создания нового элемента `div`, и устанавливаем его содержимое с помощью свойства `innerHTML`. Наконец, мы используем метод `appendChild()` родительского элемента, чтобы добавить новый элемент в конец списка его дочерних элементов.

Если вы хотите добавить новый элемент перед определенным элементом, можно использовать метод `insertBefore()` вместо `appendChild()`. Вот пример:

```javascript
const parentElement = document.getElementById('parent');
const existingElement = document.getElementById('existing');
const newDiv = document.createElement('div');
newDiv.innerHTML = 'Новый элемент';
parentElement.insertBefore(newDiv, existingElement);
```

В этом примере мы используем метод `getElementById()` для получения родительского элемента и существующего элемента, перед которым мы хотим добавить новый элемент. Затем мы используем функцию `createElement()` для создания нового элемента `div`, устанавливаем его содержимое, и используем метод `insertBefore()` родительского элемента, чтобы добавить новый элемент перед существующим элементом.

___
#DOM #createElement #add #createTextNode #appendChild #getElementById #browser 

___

### [[003 JSCore|Назад]]