# Unifi Network Application

Includes mongodb and all dependencies

[docker hub](https://hub.docker.com/r/joshfng/unifi-network) | [github](https://github.com/joshfng/docker-images/tree/main/unifi-network)

## Building

```shell
docker build --platform linux/amd64,linux/arm64 -t joshfng/unifi-network:9.0.92 -t joshfng/unifi-network:latest .

docker push joshfng/unifi-network --all-tags
```

## Running

Moung a volume to `/app/var` to persist server settings, backups, db, etc
