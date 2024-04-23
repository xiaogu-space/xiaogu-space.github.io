---
title : 'Mac Elasticsearch安装使用'
date : 2024-04-17T19:54:16+08:00
draft : false
image: /images/es1.png


tags: [
    "Elasticsearch"
]
---
## 安装docker

### 搜索软件包
```
brew search docker
==> Formulae
docker                                docker-machine-driver-vultr
docker-buildx                         docker-machine-nfs
docker-clean                          docker-machine-parallels
docker-completion                     docker-slim
docker-compose                        docker-squash
docker-credential-helper              dockerfile-language-server
docker-credential-helper-ecr          dockerize
docker-gen                            lazydocker
docker-ls                             powerman-dockerize
docker-machine                        dockly
docker-machine-driver-vmware          mockery

==> Casks
docker                   dockey                   dozer
docker-toolbox           dockx
```
### 安装docker
```
brew install --cask docker
```
### 注册登录，成功如下图

![](/images/docker.png)

## 安装运行Elasticsearch

使用 Docker 安装并运行 Elasticsearch

### Docker 命令安装运行
```
docker network create elastic
docker pull docker.elastic.co/elasticsearch/elasticsearch:8.13.2
docker run --name es01 --net elastic -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -t docker.elastic.co/elasticsearch/elasticsearch:8.13.2
```
### 复制生成的elastic密码和注册令牌
复制生成的elastic密码和注册令牌，它们将输出到您的终端。您将使用这些凭据在 Elasticsearch 集群中注册 Kibana 并登录。这些凭据仅在您首次启动 Elasticsearch 时显示。请自行记录。

![](/images/es4.png)

我们建议将elastic密码存储为 shell 中的环境变量。我的例子：
![](/images/es2.png)
```
export ELASTIC_PASSWORD="Pjp6q62Tc1tTUdHmgEPO"
```
### 将http_ca.crt SSL证书复制到您的计算机上
```
docker cp es01:/usr/share/elasticsearch/config/certs/http_ca.crt .
```
### 验证是否成功
使用 REST API 调用Elasticsearch以确保 Elasticsearch 容器正在运行。
```
curl --cacert http_ca.crt -u elastic:$ELASTIC_PASSWORD https://localhost:9200
```
![](/images/es3.png)

## 安装运行 Kibana

Kibana 是 Elastic 的用户界面。它非常适合初学者使用 Elasticsearch 并探索数据。我们将使用 Kibana 中的 Dev Tools 控制台向 Elasticsearch 发送 REST API 调用。

在一个新的终端会话中，启动 Kibana 并将其连接到您的 Elasticsearch 容器。
```
docker pull docker.elastic.co/kibana/kibana:8.13.2
docker run --name kibana --net elastic -p 5601:5601 docker.elastic.co/kibana/kibana:8.13.2
```
安装成功
![](/images/es5.png)
在浏览器打开 http://localhost:5601/ 并输入上面的 Configure Kibana to use this cluster Enrollment Token，并输入账号密码。
![](/images/es6.png)