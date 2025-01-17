____

tags: #emmet

_____

[Emmet](http://emmet.io/), ранее известный как Zen Coding, является самым производительным и экономным во времени плагином для текстового редактора. Простые сокращения мгновенно расширяются в сложные фрагменты кода, Emmet превратит вас в более продуктивного разработчика.  
  
## Как это работает?
  
Посмотрим правде в глаза: написание HTML-кода требует времени, со всеми тегами, атрибутами, кавычками, скобками и так далее. Конечно, в большинстве текстовых редакторов есть подсказки, которые сильно помогают, но все равно придется много печатать. 
Emmet мгновенно преобразовывает простые аббревиатуры в полноценные блоки кода.  
  
## HTML аббревиатуры
### Инициализаторы

  Подготовка к работе с новым HTML документом занимает менее чем секунду. Просто введите **!** или **html:5**, нажмите «Tab», и вы увидите HTML5 doctype с несколькими тегами и отправной точкой для вашего приложения.  
  
![](https://habrastorage.org/storage2/0a0/13d/24b/0a013d24becc519a7b9a2a55fe486f81.gif)  
  
-   **html:5** или **!** для HTML5 doctype
-   **html:xt** для XHTML transitional doctype
-   **html:4s** для HTML4 strict doctype

### Легко добавить классы, ID, текст и атрибуты

  Поскольку синтаксис Emmet для описания элементов похож на CSS селекторы, привыкнуть к нему очень легко. Попробуйте объединить название тега с идентификатором (например, **p#desc**).  
  
![](https://habrastorage.org/storage2/5b5/6bb/47a/5b56bb47a4fef147bbc5190b9a0aa429.gif)  
  
Кроме того, вы можете комбинировать классы и идентификаторы. 
Например, **p.bar#foo** выведет:  

```
<p class="bar" id="foo"></p>
```

  
Теперь давайте посмотрим, как указать содержимое и атрибуты для HTML элементов. Фигурные скобки используются для содержания. К примеру, **h1{foo}** преобразится в:  

```
<h1>foo</h1>
```
  
Квадратные скобки используются для атрибутов. Итак, **a[href=#]** выдаст следующее:  

```
<a href="#"></a>
```

  
![](https://habrastorage.org/storage2/f56/295/296/f5629529660786fd7dba68909281a0c1.gif)  
  
### Вложенность элементов

Используя вложенные сокращения, вы можете построить целую страницу, используя всего одну строку кода. Во-первых, дочерний селектор, в лице **>**, позволяет вкладывать элементы. Селектор соседних элементов, в лице **+**, позволяет размещать элементы рядом друг с другом, на том же уровне. Наконец, новый оператор перехода на уровень выше, в лице **^**, позволяет перейти по дереву элементов вверх на один уровень.  
  
![](https://habrastorage.org/storage2/575/f7b/28b/575f7b28beb25d8327f01fa104a2f620.gif)  
  
### Группировка

  Чтобы эффективно использовать вложения не превращая их в запутанный беспорядок операторов, вам нужно сгруппировать несколько кусков кода. Это как математика — нужно просто использовать скобки вокруг определенных частей.  
Например, **(.foo>h1)+(.bar>h2)** преобразится в:  

```
<div class="foo">
  <h1></h1>
</div>
<div class="bar">
  <h2></h2>
</div>
```
  
  
![](https://habrastorage.org/storage2/b6c/bc2/1d0/b6cbc21d0ff1c36829fd16ebe90491f0.gif)  
  

### Неявные имена тегов

  Чтобы объявить тег с классом, просто введите **div.item**, сокращение преобразуется в .  
В прошлом, вы могли бы опустить имя тега **div**, так что, просто нужно было ввести **.item**, и он бы генерировал . Теперь Emmet умнее. Он проверяет имя родительского тега каждый раз, когда вы разворачиваете сокращение с неявным именем.
Так что, если вы объявляете **.item** внутри , он будет генерировать  вместо . 

![[Pasted image 20221202012017.png]]

Вот список всех неявных имен тегов: 
li для ul и ol 
tr для table, tbody, thead и tfoot 
td для tr 
option для select и optgroup   

### Умножение

Вы можете определить, сколько раз элемент должен быть выведен с помощью оператора *. Например, ul>li*3 превратится в:  
<ul>   
<li></li>   
<li></li>   
<li></li> 
</ul>
### Нумерация
Как на счёт комбинации оператора умножения и нумерации? Просто поставьте оператор  в конце названия атрибута или элемента и будем вам счастье! Например **ul>li.item$*3** превратится в:    
``` <ul>   <li class="item1"></li>   <li class="item2"></li>   <li class="item3"></li> </ul> ```   
![](https://habrastorage.org/storage2/9e7/3e6/4db/9e73e64dbb039453f1a41a2c34e526b5.gif)      

## CSS аббревиатуры      
#### Значения     
Emmet предназначен для упрощения написания не только HTML, но и CSS кода. Допустим, вы хотите задать ширину. Сокращение **w100** превратится в:    ``` width: 100px; ```     ![](https://habrastorage.org/storage2/5fe/0e4/3a0/5fe0e43a060733bf095169b799e47401.gif)      

Значение px ставится по умолчанию. Другие единицы измерения используют свои символы. К примеру **h10p+m5e**:    ``` height: 10%; margin: 5em; ```     
Вот список возможных значений:    -   **p** → % -   **e** → em -   **x** → ex         

### Дополнительные опции     

Вы уже знаете много интуитивных сокращений, таких как **@f**, который преобразуется в:  
``` @font-face {   font-family:;   src:url(); } ```     
У некоторых свойств - таких как _background-image, border-radius, font, @font-face, text-outline, text-shadow_ — есть некоторые дополнительные варианты, которые вы можете активировать при помощи знака **+**. Например, **@f+** произведет:   
``` @font-face {   font-family: 'FontName';   src: url('FileName.eot');   src: url('FileName.eot?#iefix') format('embedded-opentype'),      url('FileName.woff') format('woff'),      url('FileName.ttf') format('truetype'),      url('FileName.svg#FontName') format('svg');   font-style: normal;   font-weight: normal; } ```   
![](https://habrastorage.org/storage2/1a0/999/3d1/1a09993d17f817ef88deb7232e830f4d.gif)       

### Автоматический поиск     

Модуль CSS использует автоматический поиск, чтобы найти неизвестные сокращения. 
Так, каждый раз, когда вы ищите неизвестное сокращение, Emmet попытается найти самое близкое значение. Например, **ov:h**, **ov-h**, **ovh** и **oh** произведет то же самое:  
``` overflow: hidden; ```  

![](https://habrastorage.org/storage2/175/34e/8c6/17534e8c682109a5b2cdffa03c942d01.gif)       

### Приставки браузеров     

CSS3 крут, но вендорные префиксы — реальная боль для всех нас. Теперь уже нет, Emmet нам поможет.   Например, **trs** будет преобразовано в:    ``` -webkit-transform: ; -moz-transform: ; -ms-transform: ; -o-transform: ; transform: ; ```     

![](https://habrastorage.org/storage2/421/837/254/421837254aeb306d645a81d012dc9f10.gif)      

Также вы можете приписать свои префиксы. 
Просто используйте приставку **-**. Так, **-super-foo** преобразится в:    
``` -webkit-super-foo: ; -moz-super-foo: ; -ms-super-foo: ; -o-super-foo: ; super-foo: ; ```     

Что, если вы не хотите все те приставки? Нет проблем, просто укажите первые буквы их названий.   
Например, **-wm-trf** преобразуется в:    ``` -webkit-transform: ; -moz-transform: ; transform: ; ```      -   w → -webkit- -   m → -moz- -   s → -ms- -   o → -o-         

### Градиенты     

Говоря о раздражающих особенностях CSS3, мы не можем забыть градиенты. Все те сложные выражения, что вы писали вручную, можно заменить на одну аббревиатуру.  
К примеру **lg(left, fff 50%, #000)** преобразуется в:    
~~~
``` background-image: -webkit-gradient(linear, 0 0, 100% 0, color-stop(0.5, #fff), to(#000)); background-image: -webkit-linear-gradient(left, #fff 50%, #000); background-image: -moz-linear-gradient(left, #fff 50%, #000); background-image: -o-linear-gradient(left, #fff 50%, #000); background-image: linear-gradient(left, #fff 50%, #000); ``` 
~~~
![](https://habrastorage.org/storage2/10b/0ed/234/10b0ed23401674b521c96e0f9333fad5.gif)

## Дополнительные возможности      
### Lorem ipsum     

Забудьте о сторонних сервисах, которые производят текст “Lorem ipsum”. Теперь вы можете сделать это быстро в своем редакторе. Просто используйте **lorem** или **lipsum** для сокращения. Вы можете определить сколько слов требуется вывести. 
Например, **lorem10** выведет:    ``` Lorem ipsum dolor sit amet, consectetur adipisicing elit. Libero delectus. ``` 

![](https://habrastorage.org/storage2/bf5/ed6/d4f/bf5ed6d4f37fa95e2e6e415bca911602.gif)      

Кроме того, lorem может быть присвоен к другим элементам. Например, **p*3>lorem5** преобразуется в: 
``` <p>Lorem ipsum dolor sit amet.</p> <p>Voluptates esse aliquam asperiores sunt.</p> <p>Fugiat eaque laudantium explicabo omnis!</p> ```         

## Настройка    

Emmet предлагает широкий диапазон опций, которые вы можете использовать для тонкой настройки взаимодействия с плагином. 
Есть три файла, которые Вы можете отредактировать, чтобы сделать это:    
1.  Чтобы добавить Ваш собственный или обновить существующий отрывок, отредактируйте [snippets.json](http://docs.emmet.io/customization/snippets/). 
2.  Чтобы изменить поведение фильтров и действий Emmet, попытайтесь редактировать [preferences.json](http://docs.emmet.io/customization/preferences/). 
3.  Чтобы определить, как HTML или XML должны выполняться, отредактируйте [syntaxProfiles.json](http://docs.emmet.io/customization/syntax-profiles/).      

## И намного больше!     
Это только вершина айсберга. Emmet имеет еще много других замечательных функций, таких как [кодирование и расшифровка изображений](http://docs.emmet.io/actions/base64/) **data:URL**, [обновление размеров изображения](http://docs.emmet.io/actions/update-image-size/) и [увеличение и снижение числа](http://docs.emmet.io/actions/inc-dec-number/) и т.д..   

Посетите новый [веб-сайт](http://emmet.io/), удивительную [документацию](http://docs.emmet.io/) и удобную [шпаргалку](http://docs.emmet.io/cheat-sheet/)!      

Поддерживаемые редакторы можно посмотреть на [этой странице](http://emmet.io/download/).     

**UPD**. Огромное спасибо [skaflock](https://habrahabr.ru/users/skaflock/) за помощь в исправлении ошибок.`