![Как использовать media выражения в JavaScript?](https://youtu.be/3kvKFfPteFg?t=30)

#### Ответ

![[Pasted image 20230701214544.png|600]]

*Media-выражения (Media Queries)* используются в CSS для определения стилей для разных устройств, разрешений экрана и т.д. Однако, media-выражения также могут быть использованы в JavaScript для определения, какое устройство использует пользователь, и на основе этого делать различные действия.

Для того чтобы использовать media-выражения в JavaScript, можно воспользоваться объектом `window.matchMedia()`. Этот метод возвращает объект `MediaQueryList`, который содержит информацию о том, соответствует ли текущее окно браузера заданному media-выражению.

Вот пример использования метода `window.matchMedia()`:

```javascript
const mediaQuery = window.matchMedia('(max-width: 768px)');

function handleMediaQueryChange(event) {
  if (event.matches) {
    console.log('Экран меньше 768 пикселей');
  } else {
    console.log('Экран больше 768 пикселей');
  }
}

mediaQuery.addListener(handleMediaQueryChange);
handleMediaQueryChange(mediaQuery);
```

В этом примере мы создаем объект `MediaQueryList`, который проверяет, соответствует ли ширина текущего окна браузера media-выражению `(max-width: 768px)`. Затем мы добавляем обработчик события `addListener()`, который будет вызываться каждый раз, когда состояние media-выражения изменится. В обработчике события мы проверяем, соответствует ли текущее состояние media-выражения условию `matches`, и выполняем соответствующее действие.

Также, можно использовать метод `window.matchMedia()` вместе с объектом `MediaQueryList` для проверки состояния media-выражения в любое время:

```javascript
const mediaQuery = window.matchMedia('(max-width: 768px)');

if (mediaQuery.matches) {
  console.log('Экран меньше 768 пикселей');
} else {
  console.log('Экран больше 768 пикселей');
}
```

В этом примере мы проверяем, соответствует ли текущее состояние media-выражения условию `matches`, и выполняем соответствующее действие.

___
#DOM #media-queries #matchMedia #browser #media

___

### [[003 JSCore|Назад]]