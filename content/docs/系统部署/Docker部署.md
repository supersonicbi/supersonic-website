+++
title = "Docker部署"
weight = 1
+++

# 部署前提

下载安装Docker和Docker Compose

# 启动部署
1. 进入docker目录，执行脚步启动
`
docker-compose up -d
`
支持按SuperSonic版本启动：
`
SUPERSONIC_VERSION=0.9.2-SNAPSHOT docker-compose up -d
`
{{< figure src=/img/docker_ps.png#center >}}

2. 运维操作  
查看进程运行状况：
`
docker-compose ps
`
正常会出现三个服务：
{{< figure src=/img/docker_service.png#center >}}

3. 访问：http://localhost:9080