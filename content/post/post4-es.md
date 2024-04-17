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

## 安装Elasticsearch

使用 Docker 安装并运行 Elasticsearch

* 运行以下 Docker 命令
```
docker network create elastic
docker pull docker.elastic.co/elasticsearch/elasticsearch:8.13.2
docker run --name es01 --net elastic -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -t docker.elastic.co/elasticsearch/elasticsearch:8.13.2
```

* 复制生成的elastic密码和注册令牌，它们将输出到您的终端。您将使用这些凭据在 Elasticsearch 集群中注册 Kibana 并登录。这些凭据仅在您首次启动 Elasticsearch 时显示。

    我们建议将elastic密码存储为 shell 中的环境变量。我的例子：

![](/images/es2.png)
```
export ELASTIC_PASSWORD="b5OyfgBHvYzaRX-ID+eK"
```
* 将http_ca.crt SSL证书复制到您的计算机上
```
docker cp es01:/usr/share/elasticsearch/config/certs/http_ca.crt .
```
* 使用 REST API 调用Elasticsearch以确保 Elasticsearch 容器正在运行。
```
curl --cacert http_ca.crt -u elastic:$ELASTIC_PASSWORD https://localhost:9200
```
![](/images/es3.png)