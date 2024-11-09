# VKCTF
---
**<h2>devops 300k/s</h2>**

**Описание:** Внимательно изучите конфигурацию веб-сервера и его окружение. Где-то в настройках может прятаться уязвимость, которая откроет вам доступ к скрытым данным. Сможете ли вы воспользоваться ошибкой в настройках и добраться…
<br><br>

Переходим на сайт и не наблюдаем полей ввода или частей с чем можно взаимодействовать 
![image](https://github.com/user-attachments/assets/8bba30b3-e773-4cf8-9577-8d6fc997a1f2)

в сурсах есть обфусцированный JSFUCK код:

![image](https://github.com/user-attachments/assets/29a98171-e130-4f50-bfa1-318f1f4b1a5d)

который не имеет значения

![image](https://github.com/user-attachments/assets/a74027e6-1e94-4faa-b1be-bf537d4b2b62)

поэтому идем дальше, смотрим исходный код, в котором видим flag.txt в корневом каталоге приложения и конфиг nginx, в котором допущена ошибка определения пути алиаса, которая привела к path traversal:

![image](https://github.com/user-attachments/assets/d1eb7712-d2ae-4dce-9443-ef58d609ed00)

![image](https://github.com/user-attachments/assets/57e21803-13be-4eca-adb8-845e65b6a9c4)
<br>

**<h2>Просто найди его</h2>**
**Описание:** Иногда достаточно задать правильный вопрос, чтобы раскрыть все тайны. Ваша задача — найти скрытый эндпоинт, который поможет вам обнаружить нечто важное. Сможете ли вы найти нужные запросы и извлечь важные данные из системы?


На сайте мы можем получить случайное напутствие по нажатию на кнопку
всю работу делает скрипт:
![image](https://github.com/user-attachments/assets/9db3ca02-3d6b-4bfc-83ab-4d9b7183b8e2)

переходим по ручке /graphql и наблюдаем интерфейс Graphql

![image](https://github.com/user-attachments/assets/a6d24330-6a1d-43de-b854-05d4d8c567ce)

в документации обнаруживаем способ отобразить все доступные нам типы:

![image](https://github.com/user-attachments/assets/ab063552-bb33-471b-b370-7598fc09c3fc)
![image](https://github.com/user-attachments/assets/bac60384-702a-4eaa-b9de-9a7c913276ef)

немного модифицируем запрос и посмотрим все доступные типы с полями:
![image](https://github.com/user-attachments/assets/ac543998-3c65-4451-bad3-33a5dcc862f0)

находим в типе Query поле getFlag и пробуем обратиться к нему:
![image](https://github.com/user-attachments/assets/7992436d-30c8-42b0-bbc3-14efc3f482c4)
добавляем нужный аргумент и получаем флаг:
![image](https://github.com/user-attachments/assets/8a68b5b1-d9df-43ef-9295-cffbb9151825)


**<h2>BindMaster</h2>**
**Описание:** Погрузитесь в мир неочевидных уязвимостей и исследуйте возможности системы там, где их никто не ожидал.

на сайте нас встречает форма авторизации. регистрируемся:

![image](https://github.com/user-attachments/assets/2a49b3c6-e7a2-4152-a6cf-2799629f6d80)
проверяем ручку docs и понимаем что сайт на фреймворке fastapi
![image](https://github.com/user-attachments/assets/a188df3c-5ffe-4e88-b09a-bd070c16a992)
так просто он нам не достанется
![image](https://github.com/user-attachments/assets/0af51a22-1c1f-409f-8edf-4ef65239e7c1)

на странице обращаем внимание на роль user и форму смены пароля

![image](https://github.com/user-attachments/assets/f5570836-1494-4422-a7e8-e8c0b6d5a2f7)
![image](https://github.com/user-attachments/assets/b5784b39-b639-449e-8180-8888ea121ebd)

в docs находим необязательный параметр для смены пароля
![image](https://github.com/user-attachments/assets/af43908a-d03e-47cd-a98e-2a39cf7bd3fc)

перехватываем запрос и добавляем роль

![image](https://github.com/user-attachments/assets/fb8eafda-191d-44c1-9247-62dbe5e65776)
![image](https://github.com/user-attachments/assets/df43eebe-2125-4ad1-a2a2-97b15859885b)

теперь мы можем взять флаг
![image](https://github.com/user-attachments/assets/bbc544ae-0887-4d71-9a06-c092329937d3)













