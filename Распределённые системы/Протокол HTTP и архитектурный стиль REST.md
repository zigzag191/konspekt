Методы HTTP:
- GET
- POST
- DELETE
- PUT
- HEAD
- OPTIONS

Заголовки:
- Кодировка и компрессия
- Размер
- Параметры
- Cookies
- Авторизация и аутентификация
- Ограничения по актуальности (дата истечения, Etag)
- Пользовательские параметры

Пример запроса:
```
GET index.html HTTP/1.1
Authorization: XvfSujjsss66W/=
Accept: text/plain; q=0.5, text/html, text/x-dvi; q=0.8
Host: www.relex.ru
Cookie: SID=31d4d96e407aad42;
lang=en-US
```

Пример ответа:
``` html
HTTP/1.1 200 OK
Set-Cookie: SID=31d4d96e407aad42;
Path=/;
Domain=example.com
Cache-Control: max-age=0

<HTML>
...
</HTML>
```

Через протокол HTTP реализуется стиль взаимодействия REST: [[REST API]]