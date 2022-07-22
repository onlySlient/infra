# codefever

> <https://github.com/PGYER/codefever>

## docker install

```shell
docker run -d --privileged=true --name codefever -p 8100:80 -p 23:22 --restart always -it pgyer/codefever-community:latest /usr/sbin/init
```

## docker-compose install

```yaml
version: "3.9"

networks:
  infra:
    name: infra

services:

  codefever:
    image: pgyer/codefever-community-lite:latest
    ports:
      - "8100:80"
      - "23:22"
    depends_on:
      - db
    volumes:
      - /infra/codefever/git/git-storage:/data/www/codefever-community/git-storage
      - /infra/codefever/git/logs:/data/www/codefever-community/application/logs
    environment:
      DB_HOST: "db"
      DB_PORT: "3306"
      DB_USER: "root"
      DB_PASS: "123456" # Need to be the same as MYSQL_ROOT_PASSWORD
      DB_NAME: "codefever_community"

  db:
    image: mysql:5.7.31
    restart: always
    #privileged: true
    volumes:
      - /infra/codefever/mysql:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: "123456"
    command:
      [
        '--character-set-server=utf8mb4',
        '--collation-server=utf8mb4_general_ci',
        '--max_connections=3000'
      ]
```

## validate git connect

> connect 23 port failed: close failed: password is need, but here has ssh key config.
