![Из чего состоит `HTTP`-запрос?](https://youtu.be/w-vUj0gHGgg?t=483)


#### Ответ

![[Pasted image 20230703190730.png|600]]

*HTTP-запрос* состоит из трех основных частей: строки запроса (`request line`), заголовков запроса (`request headers`) и тела запроса (`request body`), который может отсутствовать в некоторых типах запросов.

1. *Строка запроса* (`request line`) - это первая строка в HTTP-запросе, которая содержит три элемента: метод запроса (`HTTP-метод`), URI (`Uniform Resource Identifier`) и версию протокола HTTP. Например:
    
```http
    GET /index.html HTTP/1.1
```
    
2. *Заголовки запроса* (request headers) - это набор строк, которые передаются после строки запроса и содержат метаданные о запросе, такие как тип и длина содержимого, тип и версия браузера, язык пользователя и т.д. Заголовки разделяются символом перевода строки (CRLF). Например:
    
```http
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
```
    
3. *Тело запроса* (`request body`) - это необязательная часть запроса, которая содержит данные, передаваемые на сервер. Тело запроса может использоваться в запросах типа POST, PUT, DELETE и т.д. Например:
    
```http
    POST /form.php HTTP/1.1
    Host: example.com
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 25
    
    name=John&age=30&email=test@example.com
```
    

Запрос может содержать как только строку запроса и заголовки, так и все три части вместе.

Подробнее: [[3.1 HTTP простым языком|HTTP]] , [[3.2 Обзор протокола HTTP|Обзор протокола HTTP]]

___
#HTTP #HTTP-запрос #browser

___

#### [[000 Browser|Назад]]