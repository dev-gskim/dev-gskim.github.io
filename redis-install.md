# redis

### docker install

* [docker hub](https://hub.docker.com/_/redis/)

```text
# docker pull redis
# docker volume create redis
# docker network create redis-net
# docker run --name redis2020 -v redis:/data -p 6379:6379 --network redis-net -d redis redis-server --appendonly yes

### redis-cli
# docker run -it --network redis-net --rm redis redis-cli -h redis2020

### bash
# docker exec -it redis2020 bash
```

