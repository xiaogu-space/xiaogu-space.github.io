---
title: 'Mac安装GeoServer'
date: 2024-04-10T10:13:32+08:00
draft: false
image: /images/geoserver.png
---

**1.搜索是否可用安装包**
```
brew search geoserver

==> Formulae
geoserver                                         geckodriver
```
**2.安装 geoserver**
```
brew install geoserver
```
**3.成功之后查看信息,显示安装的是2.25.0版本**
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
**4.启动geoserver**
```
geoserver path/to/data/dir
```
**5.浏览器访问**

默认账号：admin,密码：geoserver

http://localhost:8080/geoserver/web

![](/images/geoserver-web.png)
