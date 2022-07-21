# codefever

> <https://github.com/PGYER/codefever>

## docker install

```shell
docker run -d --privileged=true --name codefever -p 8100:80 -p 23:22 --restart always -it pgyer/codefever-community:latest /usr/sbin/init
```

## docker-compose install

```yaml
version: "3.2"

networks:
  infra:
    name: infra

services:
  tdengine:
    image: pgyer/codefever-community:latest
    container_name: "codefever"
    restart: always
    hostname: codefever
    networks:
      - infra
    ports:
      - "8100:80"
      - "23:22"
    volumes:
      - "/infra/codefever/mysql:/var/lib/mysql"
```
