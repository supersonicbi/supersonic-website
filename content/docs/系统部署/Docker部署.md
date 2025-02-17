+++
title = "Docker部署"
weight = 2
+++

# 部署前提
下载安装Docker和Docker Compose，并启动docker  
Docker版本：26.0.0+  
Docker Compose：v2.26.1+

{{< hint info >}}
**注意**

1 如果报如下错:  
Cannot connect to the Docker daemon at unix:///Users/lexluo/.docker/run/docker.sock. Is the docker daemon running?   
说明docker没有启动

2 supersonic_db_init主要作用是数据库数据初始化，不是常驻服务。执行完成后，exited是正常现象。

{{< /hint >}}


# 启动部署
## 进入docker目录，执行脚步启动
`
    docker-compose up -d
`
{{< hint info >}}
**注意**
支持按SuperSonic版本启动，不指定版本默认是：latest  
`
SUPERSONIC_VERSION=0.9.2-SNAPSHOT docker-compose up -d
`
{{< /hint >}}

{{< figure src=/img/docker_ps.png#center >}}


{{< hint info >}}
**注意**
镜像下载慢，可配置国内镜像源，许多国内的云服务提供商提供了Docker镜像加速服务。你可以配置Docker使用这些镜像源来加速下载。
以阿里云为例：
1. 登录阿里云控制台，进入容器镜像服务。
2. 在左侧导航栏中选择“镜像加速器”。
3. 复制加速器地址，例如 https://<your-accelerator-id>.mirror.aliyuncs.com。
4. 编辑 Docker 配置文件 /etc/docker/daemon.json，添加以下内容：  
{
"registry-mirrors": ["https://<your-accelerator-id>.mirror.aliyuncs.com"]
}  
5. 重启 Docker 服务：  
sudo systemctl daemon-reload  
sudo systemctl restart docker

{{< /hint >}}

## 运维操作
1 查看进程运行状况：  
`
docker-compose ps
`
正常会出现三个服务：
{{< figure src=/img/docker_service.png#center >}}

2 查看进程日志信息：  
`
docker exec -it supersonic_standalone bash
`

进入logs目录查看日志
`
cd logs
`


## 验证
待各服务成功启动后，访问链接：http://localhost:9080  
如果无法打开链接，请尝试升级Docker Compose到26.0.0+ 、Docker版本到26.0.0+ 