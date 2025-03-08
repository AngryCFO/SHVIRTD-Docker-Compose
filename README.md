# Домашнее задание по занятию "Оркестрация группой Docker контейнеров на примере Docker Compose." - `Александра Бужор`

**Задача 1**

Сценарий выполнения задачи:

- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.

- Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: {"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}

- Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
скачайте образ nginx:1.21.1;

- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:

'''

<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>

'''

- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).

- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .


**Решение 1**


Проверяем наши версии docker и docker compose

Скачиваем к себе docker image nginx 1.21.1

![image](https://github.com/user-attachments/assets/4ed9a520-9129-46a6-ab10-744e5c1e9b5e)

Создаем репозиторий на докер-хаб

![image](https://github.com/user-attachments/assets/fd95b4a7-7566-4f11-9578-cada5715e0f7)

Собираем свой Dockerfile

![image](https://github.com/user-attachments/assets/8d36964f-e18c-4813-9f8c-e6bbb62529b1)

Создаем привественную веб страницу, котору будем подменять внутри контейнера nginx

![image](https://github.com/user-attachments/assets/d6ebf6da-6aab-460c-8aa3-99180d7658ff)

Собираем нужный нам образ с нужной веб страницей

![image](https://github.com/user-attachments/assets/720b988f-23bf-4253-892a-42633d537bf5)

Проверямем что браз наш есть в спике docker image

![image](https://github.com/user-attachments/assets/3cef25b5-fd20-4491-9294-4e468bc480f7)

Авторизуемся в докер-хаб и пушим наш собранный контейнер nginx с тегом

![image](https://github.com/user-attachments/assets/b862aadd-1eb3-4b00-ae41-ce4787332648)

Возвращаемся в докер-хаб, и видим что наш образ докера с нашим тегом успешно загружен на докер-хаб

![image](https://github.com/user-attachments/assets/7c2400ef-1a8b-45b0-bded-5801c15fe33e)


**Задача 2**

1) Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:

- имя контейнера "ФИО-custom-nginx-t2"

- контейнер работает в фоне

- контейнер опубликован на порту хост системы 127.0.0.1:8080

2) Не удаляя, переименуйте контейнер в "custom-nginx-t2"

3)Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html

4) Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.



**Решение 2**

Запускаем собранный в предыдущем задании контейнер с фоне с моей фамилией в названии, и вешаем на порт 8080

![image](https://github.com/user-attachments/assets/69bc5ee5-f642-4b00-b903-2df49e30b7ea)

Потом перименовывем контейнер, и далее выолняем команды, которые нас просят в задании

![image](https://github.com/user-attachments/assets/a779425f-6086-48f2-a88a-bcf306786fa5)

И теперь попробуем через curl дернуть нашу локальную веб-страницу из запущенного на порту 8080 контенйера nginx

![image](https://github.com/user-attachments/assets/08664820-ff54-4028-85c4-9e03303f535f)

**Задача 3**

1) Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".

2) Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.

3) Выполните docker ps -a и объясните своими словами почему контейнер остановился.

4) Перезапустите контейнер

5) Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.

6) Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.

7) Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".

8) Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 && curl http://127.0.0.1:81.

9) Выйдите из контейнера, набрав в консоли exit или Ctrl-D.

10) Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.

11) Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. пример источника

12) Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)


В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

**Решение 3**

Подключаемся к контейнеру через docker attach

![image](https://github.com/user-attachments/assets/722b6f13-a4e6-4e69-b19c-f363d70dcf2a)

Видим вывод потока. нажимаем ctrl+c и у нас завершается работа контейнера, т.к ctrl+c это стандарный сигнал заврешения процесса, чтобы контейнер работал в фоне, нужно установить ключи -d, -itБ и тогда мы просто отклбчимся от него а не заврешим.

![image](https://github.com/user-attachments/assets/b883cc98-5815-4fd4-94de-f7ef6c113fc7)

Перезапускаем контейнгер уже с ключом -it, через exec проваливаемся в него и выполняем сначал обновление компоеннтов из репозиториев, а далее ставим редактор nano для комофртного редактирования конфига nginx

![image](https://github.com/user-attachments/assets/ed2154dc-949e-4fb5-abb3-842c987f3c4b)

Изменяем внутри конфига прослушиваемый порт с 80 на 81 

![image](https://github.com/user-attachments/assets/6203fa97-9aa6-4e76-a709-02121d5a852e)

Теперь перезапускаем nginx для применения конфигурации и дергаем curlom старый порт и новый порт 

![image](https://github.com/user-attachments/assets/ce1fac7c-990a-4148-8e12-6b12d9cec3f1)

Видим что с 81 порта мы можем получить ответ на запрос

Теперь выйдем из контейнера и попробуем дернуть по 8080 наш nginx, то получаем ошибку.

![image](https://github.com/user-attachments/assets/93e3dabf-5e22-417a-8e24-4018c9a5597d)

ПОЧЕМУ?

та потому что при запуске мы указывали что 80 порт нашего контейнера прокидывается на 8080 порт машины, а сейчас мы просто поменяли 80 на 81 не перепроросив 81 порт на порт 8080, вот и вся проблема.

Так как контейнерм "мы сломали" ))) он на мбольше не нужен, то мы его удаляем, и не просто так, а без остановки, т.е. на горячуюю, для этого нам нужен будет ключ -f (force)

![image](https://github.com/user-attachments/assets/1427be79-e1ff-496d-ae4a-006b730801b6)

и через docker ps -a убеждаемся что контейнер грохнули окончательно


**Задача 4**

- Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку текущий рабочий каталог $(pwd) на хостовой машине в /data контейнера, используя ключ -v.

- Запустите второй контейнер из образа debian в фоновом режиме, подключив текущий рабочий каталог $(pwd) в /data контейнера.

- Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.

- Добавьте ещё один файл в текущий каталог $(pwd) на хостовой машине.

- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.



**Решение 4**


Запускаем 2 конетейнера с разными операционаками, и прбрасываем нашу текущуб директорию нашей рабочей ОС внктрь обоих контейнеров в каталог data

![image](https://github.com/user-attachments/assets/ebf8c48d-f698-4524-a75e-4bece0ed6e09)

Теперь через exec провалимся внутрь каждого контейнера и создадим там file1 через контейнер centos, и file2 через debian

В итоге мы можем заметить, что в какой бы контейнер бы не заходили в папку дата, эти оба файла создаются в докальной директории на нашей хостовой машине

![image](https://github.com/user-attachments/assets/9573a16d-97ee-4b05-866b-2607e7f23ec6)

![image](https://github.com/user-attachments/assets/dab3dd15-5813-48e0-905d-02b5fead2553)

**Задача 5**

1) Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него. "compose.yaml" с содержимым:

'''
version: "3"
services:
  portainer:
    image: portainer/portainer-ce:latest
    network_mode: host
    ports:
      - "9000:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      '''
"docker-compose.yaml" с содержимым:

'''
version: "3"
services:
  registry:
    image: registry:2
    network_mode: host
    ports:
    - "5000:5000"

  '''

И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )

2) Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)

3) Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/

4) Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)

5) Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:

'''

version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
      '''
      
6) Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".

7) Удалите любой из манифестов компоуза(например compose.yaml). Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.

**Решение 5**

Если запущен контейнер portainer, это означает, что был использован файл compose.yaml. Если запущен контейнер registry, это означает, что был использован файл docker-compose.yaml.

На практике, поведение Docker Compose может зависеть от версии и конфигурации.

![image](https://github.com/user-attachments/assets/1b36b144-be82-4bd5-af7e-a4bdb8adc15c)

Теперь отредактирую файлик compose.yaml

![image](https://github.com/user-attachments/assets/aadcfb7b-2dfd-4302-8565-4f6d07471918)

И проверим что завелись оба контейнера 

![image](https://github.com/user-attachments/assets/ebf6096e-899b-4f42-98c7-41ec09572bf7)

Помечаем ранее созданный кастомный образ и пушим его 

![image](https://github.com/user-attachments/assets/0432f878-9a05-42b9-8e3f-1e625a23223b)

сейчас проверим что у на сработает локальный репозиторий

Дропнем localhost:5000/custom-nginx

Подтянем его с локлаьной репы

Проверим есть ли localhost:5000/custom-nginx в нашем списке

![image](https://github.com/user-attachments/assets/28e93444-be41-4e20-9032-edc166b9cb56)

Теперь зайдем на веб-интерфер Portnainer

![image](https://github.com/user-attachments/assets/724fd366-61df-4b95-9d40-a4a3279564d3)

Запустим compose-nginx через веб интерфейс

![image](https://github.com/user-attachments/assets/9469271c-1227-4cac-bfde-dfc7f3fd4c6d)

Зайдем в консоль машины и увидем что контейнер запустился 

![image](https://github.com/user-attachments/assets/b67e5cd3-809a-4e35-8c1b-ffd8f9167662)

Далее по заданию делаем снимок контейнера в portainer от от поля AppArmorProfile до Driver

![image](https://github.com/user-attachments/assets/c2510c95-d03b-4067-81c5-ee7c04a094ed)

Теперь удалим compose.yaml и попробуем прогнать docker compose up -d. И сразу видим предупреждение что найдены потерянные контейнеры для этого проекта.
Описание контейнера Portainer было в удалённом файле compose.yaml, можно запустить команду с флагом --remove- orphans, чтобы очистить ее.

![image](https://github.com/user-attachments/assets/c67fd63a-73c5-4f36-9369-33a2a6b6dae3)

И теперь останавливаем все контейнеры одной командой

![image](https://github.com/user-attachments/assets/638ed461-76aa-496d-801e-7a9d6b13e986)

И удостоверимся, что все контейнеры выключены 

![image](https://github.com/user-attachments/assets/1d984f48-88a4-4081-84c1-018b18ebcf3b)
