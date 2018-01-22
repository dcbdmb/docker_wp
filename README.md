# URL's as reference
https://buddy.works/guides/wordpress-docker-kubernetes-part-1?utm_source=newsletter&utm_medium=email&utm_campaign=n_3817

https://docs.docker.com/engine/reference/commandline/docker/#child-commands

## Docker commands
> vi Dockerfile
FROM wordpress:php7.1-apache

> docker buid -t 'wp_image' .

> docker run --name mysql-cont -e MYSQL_ROOT_PASSWORD=qwerty -d mysql:5.7

> docker run --name wp-cont --link mysql-cont:mysql -p 8000:80 -d wp-image

> all in 1 command: docker run --name wp-cont -e WORDPRESS_DB_HOST=host:port -e WORDPRESS_DB_USER=user -e WORDPRESS_DB_PASSWORD=pass -p 8000:80 -d wp-image

> docker stop wp-cont

> docker stop mysql-cont

> docker start wp-cont

> docker start mysql-cont

> docker restart wp-cont

> docker restart mysql-cont

### See the results
in browser type: http://127.0.0.1:8000

## Using docker compose
> vi docker-compose.yml
```
version: '3'
services:
  wp:
    build: .
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_PASSWORD: qwerty
  mysql:
    image: "mysql:5.7"
    environment:
      MYSQL_ROOT_PASSWORD: qwerty
```

> docker-compose up -d

###See the results###
> http://127.0.0.1:8000

> docker-compose down

> docker-compose up -d --build

#To persist data:
version: '3'
services:
  wp:
    build: .
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_PASSWORD: qwerty
  mysql:
    image: "mysql:5.7"
    environment:
      MYSQL_ROOT_PASSWORD: qwerty
    volumes:
      - my-datavolume:/var/lib/mysql
volumes:
  my-datavolume:

###To push your own docker images:###
1. Sign up on docker hub
2. > docker built -t my-docker-hub-username/my-image .
3. > docker push my-docker-username/my-image

update docker-compose to:
version: '3'
services:
  wp:
    image: "my-docker-hub-username/my-image"
    ports:
      - "80:80"
    environment:
      WORDPRESS_DB_PASSWORD: qwerty
  mysql:
    image: "mysql:5.7"
    environment:
      MYSQL_ROOT_PASSWORD: qwerty
    volumes:  
      - "my-datavolume:/var/lib/mysql"
volumes: 
  my-datavolume:

> docker-compose up -d

## Next Step
https://buddy.works/guides/how-run-wordpress-on-kubernetes?utm_source=newsletter&utm_medium=email&utm_campaign=ns_4417
