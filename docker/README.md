# Docker


## Build

```bash
docker build -t <IMAGE NAME>:<TAG> .  
eg: docker build -t kubia
#  创建image
# -t： 给image加一个tag 
# . ： 以当前目录，要有Dockerfile
```

## tag

```bash
docker tag <LOCA_IMAGE_NAME>:<TAG> <DOCKERHUB_USERNAME>/<LOCA_IMAGE_NAME>:<TAG>
eg: docker tag kubia:latest yli2935/kubia:latest
# 标记本地镜像，将其归入某一仓库
# 本地镜像 <LOCA_IMAGE_NAME>:<TAG>
# 目标仓库： <DOCKERHUB_USERNAME>
```

## push

```bash
docker push <DOCKERHUB_USERNAME>/<LOCA_IMAGE_NAME>:<TAG>
eg: docker push yli2935/kubia:latest
# push image到云端仓库
# 目标仓库： <DOCKERHUB_USERNAME>
```

