# Docker

## Prune
Remove all unused images not just dangling ones. also it will remove all build cache
```
docker system prune -a
```

## Delete all stopped instances
```
docker rm $(docker ps -a -q)
```
