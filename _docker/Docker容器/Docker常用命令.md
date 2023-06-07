---
layout: default
title: Docker常用命令
parent: Docker容器
nav_order: 2
---

# docker build
1. 作用：用于构建docker镜像的指令
2. 指令格式：`docker build [OPTIONS] PATH | URL | -`
```shell
# 示例一 docker build [OPTION] PATH
docker build -t <IMAGE_NAME>:<TAG> PATH
docker build -t test1:v1.0.0.1 .
docker build -t test1:v1.0.0.1 ./docker
# 示例二 docker build [OPTION] URL
docker build -t <IMAGE_NAME>:<TAG> URL
docker build -t test2:v1.0.0.2 github.com/creack/docker-firefox
# 示例三 docker build [OPTION] -
docker build -t <IMAGE_NAME>:<TAG> -
docker build -t test3:v1.0.0.3 - < Dockerfile
docker build -t test3:v1.0.0.3 - < /mnt/docker/Dockerfile1
docker build -t test3:v1.0.0.3 - < context.tar.gz
```

3. 注意事项
:::info

- 当用PATH进行构建时，PATH指定了构建时的上下文的的文件位置
- PATH里需要包含Dockerfile，而且会把当前目录的所有文件上传到docker守护程序
- PATH可以是一个目录
- 当用URL时，若URL是git仓库链接，则会使用`git clone --recursive`命令递归的克隆仓库及其子模块的内容
- URL还可以是一个标准的TAR压缩包
- 当使用 - 模式时，将会从STDIN读取Dockerfile，并且没有上下文，所以进行`ADD`指令操作时，只能通过引用的方式添加文件
- - 模式也可以支持TAR包
:::
# docker cp

1. 作用：从容器复制文件到本地，或者从本地复制文件到容器
2. 指令格式：
   1. `docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-`
   2. `docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH`
```shell
# 容器文件复制到本地 docker cp <CONTAINER_NAME> | <CONTAINER_ID>:/FILE_NAME /LOCAL_PATH/
docker cp test:/myvol/greeting ./myvol/
docker cp 15dade8190d1:/myvol/greeting ./myvol/greeting
# 本地文件复制到容器docker cp /LOCAL_PATH/FILE <CONTAINER_NAME> | <CONTAINER_ID>:/FILE_NAME
docker cp ./myvol/test.txt test:/myvol
docker cp ./myvol/test.txt 15dade8190d1:/myvol
# 将容器文件作为TAR存档流式输出到本地
docker cp test:/myvol/greeting - > test.tar

```
> - 当SRC_PATH是一个文件时有如下情况：

|  | **以'/'结尾** | **不以'/'结尾** | **是一个文件** | **是一个文件夹** |
| --- | --- | --- | --- | --- |
| **DESTPATH不存在** | 报错：目标目录必须存在 | 内容保存在创建的destPath中 |  |  |
| **DESTPATEH存在** |  |  | 目标文件的内容将被源文件覆盖 | 源文件将被复制到目标目录下 |

> - 当SRC_PATH是一个文件夹时有如下情况：

|  | **是一个文件** | **是一个文件夹** |  |
| --- | --- | --- | --- |
| **DESTPATH不存在** |  | 创建目标目录并将源目录的内容复制到此处 |  |
| **DESTPATEH存在** | 报错：不能将目录复制到文件 | **SRC以'/.'结尾** | **SRC不以'/.'结尾** |
|  |  | 源目录的内容被复制到目标目录 | 源目录被复制到目标目录 |

# docker exec

1. 作用：用于在运行的容器中执行命令
2. 指令格式：`docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`
```shell
# 连接到正在运行的容器并分配一个伪TTY(相当于命令终端)
# docker exec -it <CONTAINER_NAME> | <CONTAINER_ID> /bin/bash | bash | <OTHER_SHELL>
docker exec -it test /bin/bash
docker exec -it -e VAR=1 test /bin/bash
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--detach, -d` | 后台执行命令 |
| `--detach-keys` | 覆盖用于分离容器的键序列 |
| `--env, -e` | 设置环境变量 |
| `--env-file` | 读取环境变量文件 |
| `--interactive, -i` | 保持STDIN打开，即使未连接 |
| `--privileged` | 为命令授予扩展权限 |
| `--tty, -t` | 为命令分配TTY |
| `--user, -u` | 为命令指定用户 |
| `--workdir, -w` | 指定命令在容器中执行的工作目录 |

# docker history

1. 作用查看镜像的构建过程
2. 指令格式：`docker history [OPTIONS] IMAGE`
```shell
# docker history <image_name> | <image_id>
docker history test
docker history fa7a39ee72ff
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--format` | 以GO模板输出指定的镜像属性 |
| `--human, -H` | 以可读格式打印大小和日期 |
| `--no-trunc` | 不截断输出 |
| `--quiet, -q` | 只显示镜像的ID |

# docker images

1. 作用：查看镜像
2. 指令格式：`docker images OPTIONS IMAGE_NAME:TAG`
```shell
# 不指定tag, 则将查看tag是latest的镜像，若没有则报错
docker imgaes test
docker images test:v1
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--all, -a` | 输出所有镜像，默认是隐藏了中间镜像 |
| `--digests` | 输出摘要 |
| `--filter, -f` | 根据条件过滤输出 |
| `--format` | 以GO模板输出指定的镜像属性 |
| `--no-trunc` | 不截断输出 |
| `--quiet, -q` | 只显示镜像的ID |

# docker inspect

1. 作用：查看docker中的对象的基本信息，包括镜像，容器, 网络等
2. 指令格式：`docker inspect [OPTIONS] NAME|ID [NAME|ID...]`
```shell
# 查看镜像信息
docker inspect test
```
> 1. 如果存在容器和镜像的NAME相同，则使用此命令用NAME查看的将会是容器信息，若想查看镜像信息，需要用镜像ID查看

:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--format, -f` | 以GO模板输出指定的镜像属性 |
| `--size, -s` | 如果对象是容器，则显示总文件大小 |
| `--type` | 返回指定类型的JSON |

# docker logs

1. 作用：查看容器的日志
2. 指令格式：`docker logs [OPTIONS] CONTAINER`
```shell
docker logs test
# 显示并跟踪日志
docker logs -f test
# 显示时间戳
docker logs -t -f test
# 查询最新的前200行日志
docker logs -tf -n 200 test
# 查询从三分钟前开始的日志
docker logs -tf --since 3m test | docker logs -tf --since 2023-01-09T02:15:01 test
# 查询两分钟之前的日志
docker logs -tf --until 2m test | docker logs -tf --until 2023-01-09T02:15:02 test
# 查看过去第三分钟内的日志
docker logs -tf --since 3m --until 2m test
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--details` | 显示日志额外的详细信息 |
| `--follow, -f` | 跟踪日志输出 |
| `--since` | 查看指定时间戳之后的日志，可以指定时间戳或者相对时间(2h, 2m, 2s等) |
| `--tail, -n` | 显示最新的NUM行日志，默认是显示所有 |
| `--timestamps, -t` | 显示时间戳 |
| `--until` | 查看指定时间戳之前的日志，可以指定时间戳或者相对时间(2h, 2m, 2s等) |

# docker ps

1. 作用：查看容器列表
2. 指令格式：`docker ps [OPTIONS]`
```shell
docker ps 
docker ps -a
查看所有容器名中包含test字符串的容器
docker ps -a | grep test
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--all, -a` | 显示所有的容器，默认只显示正在运行的容器 |
| `--filter, -f` | 按照指定的条件进行过滤 |
| `--format` | 使用GO模板格式化输出 |
| `--last, -n` | 显示N个上次创建的容器，包括所有状态(默认值是-1) |
| `--latest, -l` | 显示最新创建的容器，包括所有状态 |
| `--no-trunc` | 不截断输出，会显示初容器的长ID和容器的ports |
| `--quiet, -q` | 只显示容器的ID |
| `--size, -s` | 显示容器的总文件大小 |

> - 如果容器暴露了多个端口，则ports列会显示一个范围，例如：100-102/TCP(表示100,101,102三个端口)
> - size列的显示格式为：<num1> (virtual num2)
>    - num1表示容器可写层的数据量大小
>    - num2表示的是容器对应的只读镜像的数据量大小

## 过滤选项
:::info

- 使用过滤时，可过滤的选项如下
   - **id**：容器ID，可以使用长ID，短ID或者ID的开头片段，匹配所有容器ID中以指定字符串开头的容器
      - `docker ps --filter id=2ffeb7ef2ba8`
   - **name**：容器名，匹配所有容器名中以指定字符串开头的容器
      - `docker ps --filter name=test`
   - **label**：容器标签，匹配指定的容器标签或标签值
      - `docker ps --filter "label=color"`
      - `docker ps --filter "label=color=blue"`
   - **exited**：匹配容器退出时的代码，仅在-a模式下有效
      - `docker ps -a --filter 'exited=0'`
   - **status**：容器状态，匹配指定容器的状态
      - `docker ps --filter status=running`
      - 状态值可选项：**created**、**restarting**、**running**、**removing**、**paused**、**exited**、**dead**
   - **ancestor**：匹配容器的镜像，镜像值可选项如下
      - **image**：镜像名匹配
         - `docker ps --filter ancestor=httpd`
      - **image:tag**：镜像名加版本匹配
         - `docker ps --filter ancestor=httpd:latest`
      - **image:tag@digest**：镜像名加版本加摘要匹配
         - `docker ps --filter ancestor=httpd:latest@sha256:f2e89def4c032b02c83e162c1819ccfcbd4ea6bdbc5ff784bbc68cba940a9046`
      - **short_id**：镜像短ID匹配
         - `docker ps --filter ancestor=8653efc8c72d`
      - **full_id**：镜像长ID匹配
         - `docker ps --filter ancestor=8653efc8c72daee8c359a37a1dded6270ecd1aede2066cbecd5be7f21c916770`
   - **before**：匹配在给定的容器之前创建的容器，可以通过容器ID(只支持长ID)或容器名
      - `docker ps -f before=e177d04e24e93615a9d22225d6b1b71bce4179c7541fabe840641c65fcdc5f88`
      - `docker ps -f before=blissful_hawking`
   - **since**：匹配在给定的容器之后创建的容器，可以通过容器ID(只支持长ID)或容器名
      - `docker ps -f since=e177d04e24e93615a9d22225d6b1b71bce4179c7541fabe840641c65fcdc5f88`
      - `docker ps -f since=blissful_hawking`
   - **volume**：挂载卷，匹配挂载了特定卷或在特定目录下有挂载卷的容器(容器内的目录或文件)
      - `docker ps -f volume=/myvol`
   - **network**：容器网络，匹配连接到指定的网络的容器，可以用网络ID或网络名匹配
      - `docker ps -f network=my_net1`
   - **expose**：暴露端口(暴露端口后容器之间可以访问)，匹配暴露了指定的端口或者端口范围的容器
      - `docker ps -f expose=8080`
      - `docker ps -f expose=8000-8080/udp`可以指定端口范围和协议类型
   - **publish**：发布端口(发布端口后，外部可以访问容器)，匹配发布了指定的端口或者端口范围的容器
      - `docker ps -f publish=8080`
      - `docker ps -f publish=8000-8080/udp`可以指定端口范围和协议类型
   - **health**：容器健康检查状态(starting、healthy、unhealthy、none)，匹配指定健康状态的容器
      - `docker ps -f health=none`
   - **is-task**：筛选是或不是服务任务的容器
      - `docker ps -f is-task=true`
      - `docker ps -f is-task=false`
:::
## 格式化有效占位符
:::info

- 使用格式化输出时，有效的占位符如下
   - `**.ID**`：网络ID
      - `docker ps -a --format "容器ID是：{{.ID}}"`
   - `**.Image**`：镜像ID
      - `docker ps -a --format "镜像ID是：{{.Image}}"`
   - `**.Command**`：引用的命令
      - `docker ps -a --format "引用命令是：{{.Command}}"`
   - `**.CreatedAt**`：容器创建时间
      - `docker ps -a --format "容器创建时间是：{{.CreatedAt}}"`
   - `**.RunningFor**`：容器已经启动了多久的时间
      - `docker ps -a --format "容器启动时间是：{{.RunningFor}}"`
   - `**.Ports**`：暴露的端口
      - `docker ps -a --format "暴露的端口是：{{.Ports}}"`
   - `**.State**`：容器的状态
      - `docker ps -a --format "容器的状态是：{{.State}}"`
   - `**.Status**`：容器的健康状态
      - `docker ps -a --format "容器健康状态是：{{.Status}}"`
   - `**.Size**`：容器磁盘大小
      - `docker ps -a --format "容器磁盘大小是：{{.Size}}"`
   - `**.Names**`：容器名
      - `docker ps -a --format "容器名是：{{.Names}}"`
   - `**.Labels**`：容器指定的所有标签
      - `docker ps -a --format "所有标签是：{{.Labels}}"`
   - `**.Label**`：容器单个标签
      - `docker ps -a --format "swarm.cpu标签是：{{.Label 'com.docker.swarm.cpu'}}"`
   - `**.Mounts**`：容器中的挂载卷名称
      - `docker ps -a --format "挂载卷是：{{.Mounts}}"`
   - `**.Networks**`：容器连接的网络名称
      - `docker ps -a --format "网络名称是：{{.Networks}}"`
- 一次命令可以使用多个占位符
:::
# docker pull

1. 作用：从远程仓库拉去镜像
2. 指令格式：`docker pull [OPTIONS] NAME[:TAG|@DIGEST]`
```shell
# 通过镜像名拉取
docker pull httpd
# 通过镜像名和版本(TAG)拉取
docker pull httpd:2.4
# 通过镜像名和版本以及摘要拉取
docker pull httpd:2.4@sha256:f2e89def4c032b02c83e162c1819ccfcbd4ea6bdbc5ff784bbc68cba940a9046
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--all-tags, -a` | 下载镜像所有的版本 |
| `--disable-content-trust` | 跳过镜像验证，默认为true |
| `--platform` | 如果服务器支持多平台，则可以设置平台 |
| `--quiet, -q` | 抑制详细输出 |

> - 默认是从docker Hub上拉取镜像，也可以拉取私服仓库的镜像，需要指定IP和port
>    - `docker image pull myregistry.local:5000/testing/test-image`

# docker push

1. 作用：推送镜像到远程仓库
2. 指令格式：`docker push [OPTIONS] NAME[:TAG]`
```shell
# 将容器保存为新镜像
docker container commit c16378f943fe my-httpd:v1.0.1
# 在本地仓库创建一个tag
docker image tag my-httpd:v1.0.1 registry-host:5000/myadmin/my-httpd:v1.0.1
# 将镜像推送到本地仓库
docker image push registry-host:5000/myadmin/my-httpd:v1.0.1
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--all-tags, -a` | 推送镜像所有的版本 |
| `--disable-content-trust` | 跳过镜像签名，默认为true |
| `--quiet, -q` | 抑制详细输出 |

> - 默认是推送镜像到docker Hub上，也可以推送镜像到私服仓库，需要指定IP和port
>    - `docker image push registry-host:5000/myadmin/my-httpd:v1.0.1`

# docker rename

1. 作用：给容器重命名
2. 指令格式：`docker rename CONTAINER NEW_NAME`
```shell
# 通过容器名为容器重命名
docker rename suspicious_keller httpd1
# 通过容器ID为容器重命名
docker rename 44c3eb9647b2 httpd2
```
# docker restart

1. 作用：重新启动一个或多个容器
2. 指令格式：`docker restart [OPTIONS] CONTAINER [CONTAINER...]`
```shell
docker restart httpd
docker restart 44c3eb9647b2
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--time, -t` | kill docker进程之前需要等待的秒数，默认为10 |

# docker rm

1. 作用：删除一个或多个容器
2. 指令格式：`docker rm [OPTIONS] CONTAINER [CONTAINER...]`
```shell
docker rm test
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--force, -f` | 强制删除正在运行的容器(使用SIGKILL) |
| `--link, -l` | 移除指定的容器链接 |
| `--volumes, -v` | 删除与容器关联的匿名卷 |

> - 可以使用如下命令删除指定状态的容器
>    - `docker rm $(docker ps --filter status=exited -q)`

# docker rmi

1. 作用：删除一个或多个镜像
2. 指令格式：`docker rmi [OPTIONS] IMAGE [IMAGE...]`
```shell
docker rmi test
docker rmi fd484f19954f
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--force, -f` | 强制删除镜像 |
| `--no-prune` | 不删除未被引用的父项 |

# docker start

1. 作用：启动一个或多个容器
2. 指令格式：`docker start [OPTIONS] CONTAINER [CONTAINER...]`
```shell
docker start test
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--attach, -a` | 连接到STDOUT/STDIN，并转发信号 |
| `--detach-keys` | 覆盖用于分离容器的键序列 |
| `--interactive, -i` | 连接容器的STDIN |

1. 作用：停止一个或多个容器
2. 指令格式：`docker stop [OPTIONS] CONTAINER [CONTAINER...]`
```shell
docker stop test
```
:::info

- OPTIONS参考如下：
:::
| **name** | **描述** |
| --- | --- |
| `--time, -t` | kill docker进程之前需要等待的秒数，默认为10 |

