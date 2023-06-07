---
layout: default
title: 安装Docker
nav_order: 2
---
# 安装
```shell
yum -y update
```
```shell
uname -r
```
```shell
yum install -y yum-utils
```
```shell
sudo yum remove -y docker*
```
```shell
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```
```shell
yum makecache fast
```
```shell
yum list docker-ce --showduplicates | sort -r
```
```shell
yum install -y docker-ce-3:20.10.9-3.el7.x86_64
```
注意：若发生如下错误 需要执行 yum clean all，再执行安装命令。
```shell
No Presto metadata available for docker-ce-stable
docker-ce-cli-20.10.20-3.el7.x FAILED                                          
https://mirrors.aliyun.com/docker-ce/linux/centos/7/x86_64/stable/Packages/docker-ce-cli-20.10.20-3.el7.x86_64.rpm: [Errno 14] HTTPS Error 404 - Not Found.0 B/s |    0 B  --:--:-- ETA 
Trying other mirror.
To address this issue please refer to the below wiki article 

https://wiki.centos.org/yum-errors

If above article doesn't help to resolve this issue please use https://bugs.centos.org/.

docker-ce-rootless-extras-20.1 FAILED                                          
https://mirrors.aliyun.com/docker-ce/linux/centos/7/x86_64/stable/Packages/docker-ce-rootless-extras-20.10.20-3.el7.x86_64.rpm: [Errno 14] HTTPS Error 404 - Not Found0 B  --:--:-- ETA 
Trying other mirror.


Error downloading packages:
  docker-ce-rootless-extras-20.10.20-3.el7.x86_64: [Errno 256] No more mirrors to try.
  1:docker-ce-cli-20.10.20-3.el7.x86_64: [Errno 256] No more mirrors to try.

```
```shell
systemctl start docker
```
```shell
systemctl enable docker
```
```shell
docker version
```
# 配置镜像加速源
```shell
vim /etc/docker/daemon.json
```
向daemon.json文件中键入以下内容
```shell
{
   "registry-mirrors": [
       "https://mirror.ccs.tencentyun.com"
  ]
}
```
```shell
sudo systemctl restart docker
```
