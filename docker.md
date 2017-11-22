https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes

## remover todas as imagens
```
docker rmi (docker image ls -q)
```

## Remove dangling images
```
docker rmi (docker images -f dangling=true -q)
```

## restart / parar / remover todos os containers
```
docker stop (docker ps -a -q)
docker rm (docker ps -a -q)
docker restart (docker ps -a -q)
```

## logs
```
docker logs -ft {id_do_container}
```

## logs
```
docker logs -ft {id_do_container}
```

## execute shell
```
docker exec -it {id_do_container} {shell}
```
