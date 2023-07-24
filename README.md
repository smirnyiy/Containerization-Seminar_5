Урок 5. Docker Compose и Docker Swarm
1) создать сервис, состоящий из 2 различных контейнеров: 1 - веб, 2 - БД (compose)
Задание со звездочкой - повышенной сложности..
** не обязательно 2) необходимо создать 3 сервиса в каждом окружении (dev, prod, lab)
** не обязательно 3) по итогу на каждой ноде должно быть по 2 работающих контейнера
4) выводы зафиксировать



Решение:
• Создаем директорию compose, в нее используя редактор nano добавляем файл compose.yaml:

mkdir compose
cd compose/
nano compose.yaml


содержимое файла compose.yaml (добавляем для запуска 2 сервиса, DB и phpmyadmin, оба latest версии, задаем параметры для DB и phpmyadmin, устанавливаем для phpmyadmin зависимость (depends_on):

version: '3.9'

services:
  db:
    image: mysql:latest
    environment:
      MYSQL_USERNAME: root
      MYSQL_ROOT_PASSWORD: 12345
      MYSQL_DATABASE: djc_db
  phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    restart: always
    ports:
      - 8080:80
    depends_on:
      - db
