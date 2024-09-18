# Домашняя работа к занятию «Введение в Docker» - Боровик А. А.

## Задача 1

Сценарий выполнения задачи:

- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
- Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: `{"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}`
- Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на [https://hub.docker.com](https://hub.docker.com/) (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
- скачайте образ nginx:1.21.1;
- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:

```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
```

- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).
- Предоставьте ответ в виде ссылки на [https://hub.docker.com/](https://hub.docker.com/)<username_repo>/custom-nginx/general .

### Ответ:

[Docker файл](https://github.com/Lex-Chaos/Docker-hw/blob/main/files/Docker)

[Ссылка на репозиторий docker hub](https://hub.docker.com/repository/docker/aaborovik/custom-nginx/general)


## Задача 2

1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:

- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080

2. Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду `date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080 ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html`
4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

### Ответ

1. Запуск контенера

![Запуск контенера](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task2-1-1.png)

![Запуск контенера](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task2-1-2.png)

2. Переименование контенера

![Переименование контенера](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task2-2.png)

3. Команда и доступность страницы

![Команда и доступность страницы](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task2-3+4.png)

## Задача 3

1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3. Выполните `docker ps -a` и объясните своими словами почему контейнер остановился.
4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8. Запомните(!) и выполните команду `nginx -s reload`, а затем внутри контейнера `curl http://127.0.0.1:80 ; curl http://127.0.0.1:81`.
9. Выйдите из контейнера, набрав в консоли `exit` или Ctrl-D.
10. Проверьте вывод команд: `ss -tlpn | grep 127.0.0.1:8080` , `docker port custom-nginx-t2`, `curl http://127.0.0.1:8080`. Кратко объясните суть возникшей проблемы.
11. - Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. [пример источника](https://www.baeldung.com/linux/assign-port-docker-container)
12. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

### Ответ

![1+2+3](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task3-1+2+3.png)

Контейнер остановился, потому что в его стандартный поток был послан сигнал остановки.

Зашёл в контенер с помощью команды:

```
docker exec -it custom-nginx-t2 bash
```
Установил редактор nano с помощью:

```
apt update
apt install nano
```
Отредактировал файл:

![7](https://github.com/Lex-Chaos/Docker-hw/blob/master/img/Task3-7.png)

Перезапустил nginx. Проверил доступность страницы внутри контейнера. Проверил доступность страницы с хостовой машины:

![8+9+10](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task3-8+9+10.png)

Проблема в том, что nginx работает на порту 81.

Исправил конфигурацию контейнера согласно источнику:

![11-1](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task3-11-1.png)

![11-2](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task3-11-2.png)

![11-3](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task3-11-3.png)

![11-4](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task3-11-4.png)

![11-5](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task3-11-5.png)

Удалил контейнер не останавливая:

![12](https://github.com/Lex-Chaos/Docker-hw/blob/main/img/Task3-12.png)

---
