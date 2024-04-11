---
title: 'GeoServer发布Shapefile矢量数据'
date: 2024-04-10T10:13:32+08:00
draft: false
image: /images/geoserver.png
---
## 1.Mac GeoServer 安装

**1.1 搜索是否可用安装包**
```
brew search geoserver

==> Formulae
geoserver                                         geckodriver
```
**1.2 安装 geoserver**
```
brew install geoserver
```
**1.3 成功之后查看信息,显示安装的是2.25.0版本**
```
brew info geoserver

==> geoserver: stable 2.25.0 (bottled)
Java server to share and edit geospatial data
https://geoserver.org/
/opt/homebrew/Cellar/geoserver/2.25.0 (885 files, 125.0MB) *
  Poured from bottle using the formulae.brew.sh API on 2024-04-10 at 10:15:55
From: https://github.com/Homebrew/homebrew-core/blob/HEAD/Formula/g/geoserver.rb
License: GPL-2.0-or-later
==> Caveats
To start geoserver:
  geoserver path/to/data/dir
==> Analytics
install: 39 (30 days), 106 (90 days), 360 (365 days)
install-on-request: 39 (30 days), 106 (90 days), 360 (365 days)
build-error: 0 (30 days)
```
**1.4 启动geoserver**
```
geoserver path/to/data/dir
```
**5.浏览器访问**

默认账号：admin,密码：geoserver

http://localhost:8080/geoserver/web

![](/images/geoserver-web.png)
![](/images/geoserver-web0.png)

## 2.发布shp矢量数据
**2.1 数据准备**

自己准备好shp格式数据，放到自定义数据目录下，比如：

```
/Users/xiaogu/test_data/shp/china/map.shp
```
![](/images/geoserver-web1.png)

**2.2 创建工作空间**

进入Geoserver的Web管理页面，在GeoServer中发布和部署地图数据涉及到的几个重要概念——工作空间（WorkSpace）、存储仓库（Store）、图层（Layer）和图层组(LayerGroup)等。

![](/images/geoserver-web2.png)

**工作空间** 是一个用于组织类似图层数据（数据集）的容器。常常会把某个项目或工程的相关图层数据存放到一个工作空间里。通过工作空间的使用，可以避免相同图层名的冲突。

例如，在名为country工作空间中的china图层，引用时使用的是"country:china"，这就可以与在另一个工作空间中同样名为china图层（demo:china）避免冲突。

**存储仓库** 是一实际的文件夹或数据集。在一个工作空间中可以包含几个存储仓库，因此在引用存储仓库时必须在存储仓库前加上工作空间的名称。

![](/images/geoserver-web3.png)

**新建工作空间** 单击"添加新的工作空间"，进入新建工作空间的界面，在这里需要输入工作空间的名字和命名空间URI。
在Name文本框中输入"country"，在命名空间URI文本框中输入"http://localhost:8080/geoserver/country"，然后单击"保存"按钮。

注意：工作空间名称是描述项目的标识符，它不能超过十个字符或包含空格。命名空间URI（统一资源标识符）通常可以是与你的项目关联且添加了一个用于指示工作空间的尾随标识符的URL，命名空间URI不需要解析为实际有效的Web地址。

![](/images/geoserver-web4.png)

**2.3 在工作空间添加Shapefile**
* 在GeoServer的Web管理页面窗口的左边单击"数据"中的"存储仓库"

![](/images/geoserver-web5.png)

* 点击"添加新的存储仓库"，进入新建数据源页面。在该窗口中需要确定数据源的类型。在GeoServer中，如果同时有栅格与矢量数据的话，则需要分别建立存储仓库。

   在本实践中，我们使用的是矢量文件数据，因此选择"Shapefile"，进入新建矢量数据源窗口。

![](/images/geoserver-web6.png)
![](/images/geoserver-web7.png)