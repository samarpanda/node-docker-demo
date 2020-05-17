# Node-Docker-Demo

> Containerizing node.js applications

## Docker build & run

Build the node application docker image

```shell
# build
docker build -t my-node-app .

# docker image size
docker inspect my-node-app

# run
docker run --init --rm --publish 3000:3000 my-node-app

```

## Multi-stage build & run

Build the docker image

```shell
# build
docker build -t multi-node -f multi.node.Dockerfile .

# docker image size
docker inspect multi-node

# run
docker run --init --rm -p 3000:3000 multi-node
```

## Explain docker commands

- `--init` with docker run?
- `--rm` with docker run?
