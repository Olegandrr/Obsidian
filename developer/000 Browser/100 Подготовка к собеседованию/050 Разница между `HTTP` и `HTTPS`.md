![Разница между `HTTP` и `HTTPS`?](https://youtu.be/xZLxdts7ZW4?t=31)

#### Ответ

![[Pasted image 20230703191011.png|600]]

*HTTP* и *HTTPS* - это *протоколы передачи данных в Интернете.* Основная разница между ними заключается в том, что *`HTTPS` обеспечивает защищенное соединение, в то время как `HTTP` передает данные в незашифрованном виде.*

HTTP использует стандартный порт 80 для обмена данными между клиентом и сервером, а HTTPS использует порт 443. *HTTPS использует SSL* (`Secure Sockets Layer`) или его более современную версию *TLS* (`Transport Layer Security`) *для шифрования данных, передаваемых между клиентом и сервером. Это обеспечивает защиту от подслушивания и подмены данных во время их передачи.*

*Когда вы вводите адрес сайта, начинающийся с протокола HTTPS, ваш браузер устанавливает защищенное соединение с сервером, используя `SSL/TLS`. Браузер и сервер обмениваются специальными цифровыми сертификатами, которые подтверждают подлинность сервера и обеспечивают безопасность передачи данных.*

Таким образом, HTTPS является более безопасным протоколом, чем HTTP, и широко используется для передачи конфиденциальной информации, такой как логин и пароль, данные банковских карт и т.д.

Подробнее: [[3.1 HTTP простым языком|HTTP]] , [[3.2 Обзор протокола HTTP|Обзор протокола HTTP]] , [Полное руководство по переходу с HTTP на HTTPS](https://habr.com/ru/articles/332294/)

___
#HTTP #HTTPS #SSL #TLS #browser

___

#### [[000 Browser|Назад]]