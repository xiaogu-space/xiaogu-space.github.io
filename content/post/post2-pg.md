---
title: 'Mac上安装 PostgreSQL+PostGIS '
date: 2024-04-09T08:43:57+08:00
draft: false
image: /images/5460228_3092.jpg

categories: [
    "数据库"
]
tags: [
    "PostgreSQL"
]
---

## PostgreSQL安装

### 查看可用版本，并安装
```
brew search postgresql
brew install postgresql
```
### 启动/停止
```
brew services start postgresql
brew services stop postgresql
```
### 查看安装版本
```
pg_ctl -V
psql -V
```
### 创建一个root 用户
```
psql postgres

CREATE ROLE postgres WITH LOGIN PASSWORD '123456';
ALTER ROLE postgres CREATEDB;
ALTER USER postgres WITH SUPERUSER;
```

## PostGIS安装
### 安装PostGIS
```
brew install postgis
```
### pg中安装postgis拓展
```
CREATE EXTENSION postgis
```
### 再遇到PostGIS版本升级时需要执行
```
SELECT postgis_extensions_upgrade();
```