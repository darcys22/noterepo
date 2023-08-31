# Docker

## Prune
Remove all unused images not just dangling ones. also it will remove all build cache
```
docker system prune -a
```

prune images and containers not used for more than 24 hours
```
docker image prune -a --filter "until=24h"
docker container prune --filter "until=24h"
```

## Delete all stopped instances
```
docker rm $(docker ps -a -q)
```
