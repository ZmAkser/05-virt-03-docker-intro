# Оркестрация группой Docker контейнеров на примере Docker Compose - Мелетьев Роман Андреевич

### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, <https://github.com/имя-вашего-репозитория/git-hw> или  <https://github.com/имя-вашего-репозитория/7-1-ansible-hw>).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.

Желаем успехов в выполнении домашнего задания!

### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1
Сценарий выполнения задачи:

Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: {"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}
Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
скачайте образ nginx:1.29.0;
Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:
\```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
\```
Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).
Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

---

### Решение 1

https://hub.docker.com/r/zmakser/mra_publick

---

### Задание 2

Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
имя контейнера "ФИО-custom-nginx-t2"
контейнер работает в фоне
контейнер опубликован на порту хост системы 127.0.0.1:8080
Не удаляя, переименуйте контейнер в "custom-nginx-t2"
Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

---

### Решение 2
![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_13-28.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_13-29.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_13-32.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_13-33.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_13-34.png)

---

### Задание 3

Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
Выполните docker ps -a и объясните своими словами почему контейнер остановился.
Перезапустите контейнер
Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 ; curl http://127.0.0.1:81.
Выйдите из контейнера, набрав в консоли exit или Ctrl-D.
Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.
Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. пример источника
Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.


---

### Решение 3

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_13-42.png)
![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_13-55.png)
Нажав Ctal+C мы остановили единственный работающий в контейнере сервис(nginx), и т.к. контейнеру более нечего делать, он остановился.

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_14-07.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_14-09.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_14-10.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_14-12.png)

После наших исправлений внутри контейера nginx работает на 81 порту, а в конфигурации контейера остался проброс с порта 80 на порт 8080. Соответсвенно никаких данные на 8080 не пуступают, т.к. на 80 порт внутри контейнера более ничего не передается.

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_15-07.png)

---

### Задание 4 

Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку текущий рабочий каталог $(pwd) на хостовой машине в /data контейнера, используя ключ -v.
Запустите второй контейнер из образа debian в фоновом режиме, подключив текущий рабочий каталог $(pwd) в /data контейнера.
Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.
Добавьте ещё один файл в текущий каталог $(pwd) на хостовой машине.
Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

---

### Решение 4

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_15-43.png)
![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_15-43_1.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_15-44.png)
![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_15-44_1.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_15-45.png)

---

### Задание 5

Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него. "compose.yaml" с содержимым:
/```
version: "3"
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
"docker-compose.yaml" с содержимым:
/```
/```
version: "3"
services:
  registry:
    image: registry:2

    ports:
    - "5000:5000"
/```    
И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )

Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)

Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/

Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)

Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:

version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".

Удалите любой из манифестов компоуза(например compose.yaml). Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.

---

### Решение 5

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_16-22.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-23_16-24.png)
По умолчанию обрабатывается файл compose.yaml из того каталога, откуда вызван докер компос. Файл dokcer-compose.yaml также обрабатывается в целях совместимости, но только если нет файла compose.yaml .

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-24_11-27.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-24_11-32.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-24_11-53.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-24_13-50.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-24_13-51.png)

![](https://github.com/ZmAkser/05-virt-03-docker-intro/blob/main/img/2026-06-24_13-55.png)

---