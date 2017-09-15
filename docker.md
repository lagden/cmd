## remover todas as imagens
```
docker rmi (docker image ls -q)
```

## restart / parar / remover todos os containers
```
docker stop (docker ps -a -q)
docker rm (docker ps -a -q)
docker restart (docker ps -a -q)
```

## logs
```
docker logs -ft id_do_container
```
