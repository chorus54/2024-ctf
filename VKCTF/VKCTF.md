# VKCTF
---
**devops 300k/s**

**Описание:** Внимательно изучите конфигурацию веб-сервера и его окружение. Где-то в настройках может прятаться уязвимость, которая откроет вам доступ к скрытым данным. Сможете ли вы воспользоваться ошибкой в настройках и добраться…

переходим на сайт и не наблюдаем полей ввода или частей с чем можно взаимодействовать 
![image](https://github.com/user-attachments/assets/8bba30b3-e773-4cf8-9577-8d6fc997a1f2)

в сурсах есть обфусцированный JSFUCK код:

![image](https://github.com/user-attachments/assets/29a98171-e130-4f50-bfa1-318f1f4b1a5d)

который не имеет значения

![image](https://github.com/user-attachments/assets/a74027e6-1e94-4faa-b1be-bf537d4b2b62)

смотрим исходный код, в котором видим flag.txt в корневом каталоге приложения и конфиг nginx, в котором допущена ошибка определения пути алиаса, которая привела к path traversal:

![image](https://github.com/user-attachments/assets/d1eb7712-d2ae-4dce-9443-ef58d609ed00)

![image](https://github.com/user-attachments/assets/57e21803-13be-4eca-adb8-845e65b6a9c4)



