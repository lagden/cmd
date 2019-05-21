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

## Just clean out unused data and processes
```
docker system prune

WARNING! This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all dangling images
        - all build cache
```

or

```
docker system prune --all --force --volumes

WARNING! This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all volumes not used by at least one container
        - all images without at least one container associated to them
        - all build cache
```

or

```
docker container prune  # Remove all stopped containers
docker volume prune     # Remove all unused volumes
docker image prune      # Remove unused images
```
