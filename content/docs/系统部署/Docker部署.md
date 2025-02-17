+++
title = "Docker部署"
weight = 2
+++

# Docker部署

{{< hint info >}}
SuperSonic最新版本为0.9.10，本文档介绍基于该版本的功能。
{{< /hint >}}

## 部署前提
安装Docker和Docker Compose，并启动Docker：
Docker版本：26.0.0+  
Docker Compose：v2.26.1+

{{< hint danger >}}
如果报如下错，说明docker没有启动：

Cannot connect to the Docker daemon at unix:///Users/lexluo/.docker/run/docker.sock. Is the docker daemon running?   
{{< /hint >}}


## 启动部署

### 下载docker-compose.xml文件
```
wget https://github.com/tencentmusic/supersonic/blob/master/docker/docker-compose.yml
```

### 启动docker-compose
```
docker-compose -f docker-compose.xml up -d
```

正常会启动运行两个容器：

- **supersonic_postgres**: 存储SuperSonic元数据，以及采用pgvector插件存储Embedding向量

- **supersonic_standalone**: 启动SuperSonic前后端服务

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
```
docker-compose ps
```

2 查看进程日志信息：  
```
docker exec -it supersonic_standalone bash
```

## 登陆验证
待各服务成功启动后，访问链接：http://localhost:9080  
如果无法打开链接，请尝试升级Docker Compose到26.0.0+ 、Docker版本到26.0.0+ 