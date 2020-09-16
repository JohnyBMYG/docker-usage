# Docker

Diagrams：
https://github.com/StephenGrider/DockerCasts/tree/master/diagrams

Main repository：
https://github.com/StephenGrider/DockerCasts

Completed code for the AWS React single container project:
https://github.com/StephenGrider/docker-react

Completed code for the AWS Multi Docker Project:
https://github.com/StephenGrider/multi-docker

Completed code for the Multi K8s Project:
https://github.com/StephenGrider/multi-k8s

## Section 2 Manipulating Containers with the Docker Clinet.

Docker Client(Docker Cli)
Docker Server

docker run busybox echo hi there
docker run busybox ls
docker run busybox ping google.com

列出 running 容器
docker ps

列出所有运行过的容器
docker ps --all

docker run = docker create + docker start
docker create hello-world
docker start -a 990c5971c4322d686df36c6217020e26d9eb3ff2819f722a55d6f79f8be69610
docker start -a 3d196a5dcf43

removing stopped container 移除停止的容器
docker system prune

查看日志
docker logs 990c5971c4322d686df36c6217020e26d9eb3ff2819f722a55d6f79f8be69610

关闭容器
docker stop 3d196a5dcf43 清理后关闭，有清理退出延迟
docker kill 3d196a5dcf43 立马关闭

进入容器 执行 bash
docker exec -it containerId bash
exit

## Section 3. Building Custom Images Through Docker Server

touch Dockerfile
docker build .

tag an Image 打标签
docker build -t stephengrider/redis:latest .

manual image generation 生成镜像
docker commit -c 'CMD ["redis-server"] containerID

## Section 4. Making real projects with Docker

打标签
docker build -t johnyxu/simpleweb .

运行镜像
docker run johnyxu/simpleweb

container | local network
port1 | port2

docker run -p 8080:8080 johnyxu/simpleweb
docker run -p 5000:8080 johnyxu/simpleweb

## Section 5 Docker cCompose with multiple local containers

docker build -t johnyxu/visits:latest .

docker run myimage ->
docker-compose up

后台运行
docker-compose -d

docker build . + docker run myimage ->
docker-compose up --build

docker run -d redis
docker ps
docker stop containerID

停止容器
docker-compose down

docker-compose 命令流程
启动：docker-compose up -d
docker ps
停止：docker-compose down
docker ps

restart policies

```
'no',always,on-failure,unless-stopped
```

## Section 6 Creating a Production-Grade workflow

构建命令

`docker build -f Dockerfile.dev .`
`docker run -it -p 3000:3000 ImageId`

docker run ImageId 这里是 ImageID 或者 TagName
docker run -p 3000:3000 -v /app/node_modules -v \$(pwd):/app ImageId|TagName
docker run -it -p 3000:3000 -v /app/node_modules -v \$(pwd):/app ImageId|TagName

检查配置问题
docker-compose config

docker-compose up

```bash
web_1  | > frontend@0.1.0 start /app
web_1  | > react-scripts start
web_1  | ℹ ｢wds｣: Project is running at http://172.20.0.2/
web_1  | ℹ ｢wds｣: webpack output is served from
web_1  | ℹ ｢wds｣: Content not from webpack is served from /app/public
web_1  | ℹ ｢wds｣: 404s will fallback to /
web_1  | Starting the development server...
```

添加配置

```docker
web:
  stdin_open: true
```

docker build -f Dockerfile.dev .
Successfully built bf1ff968bc0f
docker run -it bf1ff968bc0f npm run test
docker exec -it bf1ff968bc0f npm run test

Live Tests 增加 test 容器
docker-compose up --build

docker attach containerID

production: add nginx support
docker build . -> d79d0d6acf0a
docker run -p 8081:80 d79d0d6acf0a

## Section 7 Continuous Integration and deployment with AWS

travis ci setup
