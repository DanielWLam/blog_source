---
title: linux安装mysql 
---

主要是记录一下几条命令

1. 查看有没有安装过：yum list installed mysql*

2. 查看有没有安装包：yum list msql*


3. 如果没有的话，需要先下载yum repo配置文件并安装
	1. wget http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
	2. rpm -ivh mysql57-community-release-el7-9.noarch.rpm
3. 然后就是yum install mysql
4. yum install mysql-server
5. yum install mysql-devel

题外话：今天我安装的时候，似乎直接指定3.2就行了，没有执行3.1