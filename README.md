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
# Port exposed to host is 8080. Internal port used is 80. And nginx uses 80 as the default port
docker run --init --rm -p 8080:80 static-app

# Using docker bind mount. Below command mounts the /build directory inside nginx html directory
docker run --mount type=bind,source="$(pwd)"/build,target=/usr/share/nginx/html -p 8080:80 nginx:1.17-alpine

```

## Docker bind

<u>Bind mount</u>

- Bind mount are works great when you need to share data between host and container.
- Build image `docker build --tag=incrementor-bind .`
  - New image create with the tag name `incrementor-bind`
- Run container `docker run --rm --env DATA_PATH=data/num.txt --mount type=bind,source="$(pwd)"/incrementor-data,target=/src/data incrementor-bind`

<u>Volume mount</u>

- Using bind volumes containers can maintain states between runs.
- Build image `docker build --tag=incrementor-volume .`
- Run container `docker run --rm --env DATA_PATH=/data/num.txt --mount type=volume,src=incrementor-data,target=/data incrementor-volume`

## Explain all docker command attributes used

<u>Try all example commands within this directory</u>

- `--env` Passes process environment variable. For example `docker run --rm --env DATA_PATH=data/num.txt --mount type=bind,source="$(pwd)"/incrementor-data,target=/src/data incrementor-bind`. Here `DATA_PATH` is the process environment variable passed. Node application can use this data by `process.env.DATA_PATH`
- `--rm` Deletes the container after exiting the process. Try running any container with and without this flag to see the difference. For example `docker run --rm --env DATA_PATH=data/num.txt --mount type=bind,source="$(pwd)"/incrementor-data,target=/src/data incrementor-bind` deletes the container after exiting the run process, but `docker run --env DATA_PATH=data/num.txt --mount type=bind,source="$(pwd)"/incrementor-data,target=/src/data incrementor-bind` doesn't deletes the container after exiting the process
- `src` or `source` mount source directory i.e `docker run --rm --env DATA_PATH=/data/num.txt --mount type=volume,src=incrementor-data,target=/data incrementor-volume` or `docker run --rm --env DATA_PATH=/data/num.txt --mount type=volume,source=incrementor-data,target=/data incrementor-volume`
- `--init` Gracefully exits node process where listen is used

Inspired & credits to [@btholt](https://github.com/btholt) for creating & sharing [complete into to containers](https://github.com/btholt/complete-intro-to-containers)
