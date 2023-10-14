![Как выглядит поток данных в Redux-приложении?](https://youtu.be/HBSAjY-xh3k?t=706)

#### Ответ

![[Pasted image 20230704193253.png|600]]

Жизненный цикл данных в Redux включает в себя:
* Вызов [`store.dispatch(action)`](https://rajdee.gitbooks.io/redux-in-russian/content/docs/api/Store.html#dispatch)
* *Redux-стор вызывает функцию-редюсер, который вы ему передали.*
- *Главный редюсер может комбинировать результат работы нескольких редюсеров в единственное дерево состояния приложения.
- *Redux-стор сохраняет полное дерево состояния, которое возвращает главный редюсер.

____
#React #redux #action #dispatcher #reducer #store #subscriber #component 

____

### [[004 React + Redux|Назад]]