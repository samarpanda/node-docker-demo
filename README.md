# Node-Docker-Demo

> Containerizing node.js applications

## Building a nodejs app

> Build a simple nodejs application

Build the node application docker image

```shell
cd building-a-nodejs-app

# build
docker build -t my-node-app .

# docker image size
docker inspect my-node-app

# run
docker run --init --rm --publish 3000:3000 my-node-app

```

## Multi stage build

> Preparing a multi stage build process

```shell
cd multi-stage-build

# build
docker build -t multi-node -f multi.node.Dockerfile .

# docker image size
docker inspect multi-node

# run
docker run --init --rm -p 3000:3000 multi-node
```

## Serve static files using nginx

> Create application using create-react-app and serve static files using nginx

```shell
cd serve-static-files-nginx

# build
docker build -t static-app .

# run
docker run --init --rm -p 8080:80 static-app

```

## Todos?

- Explain below docke run command attributes
  - docker run `--init`
  - docker run `--rm`
