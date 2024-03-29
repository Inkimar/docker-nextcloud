# docker-nextcloud
Looking closer into nextcloud (owncloud) 

# nextcloud and docker
https://hub.docker.com/_/nextcloud

## test 0, running with sqllite 
works, setup is done by going to the localhost.8080 adding your credentials.

## test 1, running with mariadb

Looking at this example from dockerhub <p>


```
version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    image: mariadb
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    restart: always
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=
      - MYSQL_PASSWORD=
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    ports:
      - 8080:80
    links:
      - db
    volumes:
      - nextcloud:/var/www/html
    restart: always
```

My example (mapping of ports) <p>


```
version: '3.7'

volumes:
  nextcloud:
  db:

services:
  db:
    image: mariadb:10.4.8
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    restart: always
    ports:
      - 13306:3306
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=ingimar
      - MYSQL_PASSWORD=ingimar
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    ports:
      - 9080:80
    links:
      - db
    volumes:
      - nextcloud:/var/www/html
    restart: always
```

Go to localhost:9080 and fix these Settings: <p>
1. database user = nextcloud
2. Database password = ingimar
3. database name = nextcloud 
4. db:3306
