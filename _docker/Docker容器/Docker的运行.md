---
layout: default
title: Docker的运行
parent: Docker容器
nav_order: 1
---

# 容器运行命令
## 指定容器运行模式
容器一般通过docker run 运行，运行模式分为 前台模式，和后台模式
### 后台模式
```shell
# 后台模式 
docker run -d <IMAGE_NAME>
docker run -d=true <IMAGE_NAME>

#后台模式启动服务类容器
docker run -d <IMAGE_NAME> -g "daemon off"
docker run -d=true <IMAGE_NAME> -g "daemon off"

```
> 1. 以后台模式启动的容器会在启动容器的根进程退出时一同退出，若指定了--rm，则当守护进程退出或容器进程退出时，容器将被删除
> 2. 后台模式多使用于启动服务类容器例如 nginx, mysql等，后台启动这类容器时，需要加如下参数保证容器启动成功并能使用。也可以在Dockerfile中给此类服务添加CMD ["nginx", "-g", "daemon off"]命令。
> 3. 要使以后台模式启动的容器进行输入输出，需要使用网络连接或共享卷。

### 前台模式
```shell
# 常规模式
docker run <IMAGE_NAME>
# -a：设置连接到流,可设置多个，不设置将默认连接到STDOUT和STDERR
docker run -a STDIN -a STDOUT <IMAGE_NAME>
# -t：分配伪TTY，相当于一个终端
docker run -t <IMAGE_NAME>
# -i：保持STDIN打开，即使未连接，经常和-t配合使用
docker run -i <IMAGE_NAME>
# --sig-proxy=true：将所有接受的信号代理到进程，仅限在没有伪TTY时使用
docker run --sig-proxy=true <IMAGE_NAME>
```
> 1. 对于交互进程-i，-t需要一起使用，而对于需要接受标准输入的进程，则不能使用-t
> 2. 对于容器内PID为1的进程，将会忽略所有的默认操作信号，除非编码为SIGINT或SIGTERM，否则此进程不会被终止，后续可利用这一点设置容器进程的PID。

## 设置容器身份标识
### 设置容器名
```shell
docker run --name <CONTAINER_NAME> <IMAGE_NAME>
docker run --name="<CONTAINER_NAME>" <IMAGE_NAME>
```
> 1. 识别容器可以通过三种途径：
>    1. 长ID：由docker守护进程随机分配，长度64
>    2. 短ID：为长ID的前12位字符组成
>    3. 容器名：若未用--name指令指定名称会随机生成一个容器名，指定容器名后，可用容器名对容器进行操作，容器名不能重复
> 2. 默认网桥网络的容器，必须按照名称进行通信

### 输出容器ID到文件
```shell
docker run --cidfile="<FILE_PATH>" <IMAGE_NAME>
docker run --cidfile <FILE_PATH> <IMAGE_NAME>
```
> 1. 输出的文件必须是不存在的，若存在，会报错
> 2. 输出的ID是容器的长ID

### 从指定的镜像版本启动
```shell
docker run --name <CONTAINER_NAME> <IMAGE_NAME>:<VERSION>
docker run --name test ubuntu:1.0.1
```
### 从指定的镜像digest启动
```shell
docker run <IMAGE_NAME>@<DIGEST>
docker run ubuntu@sha256:f29cc619df1abd6d32c2a5ee274f7068cbc18dd6c45a7908aed0a1fea0e88028
```
> 1. 使用镜像版本或摘要来指定运行容器的镜像，可以防止镜像改动或被篡改带来的影响
> 2. 可以同时指定镜像版本和镜像摘要
> 3. 镜像摘要的格式为sha256:<UUID>
> 4. 在拉取镜像时同样可以使用镜像版本和摘要来确保拉取的镜像是自己想要的并且未被更改的
> 5. 可以使用如下命令查看镜像的摘要
>    1. docker inspect --format="{{.Id}}" <IMAGE_NAME>/<IMAGE_ID>
>    2. docker inspect -f "{{.Id}}" <IMAGE_NAME>/<IMAGE_ID>
>    3. 若镜像名与存在的容器名相同，则会优先输出容器的摘要
>    4. 镜像摘要中的UUID的前12位就是镜像ID

## 设置容器的命名空间
### 设置容器的PID Namespace

- PID Namespace：用来隔离进程，使得不同的PID Namespace中，进程可以拥有相同的进程PID。因为每个容器都默认实现了PID命名空间，所以使得每个容器内PID为1的主进程在主机上拥有不同的PID，从而实现了不同容器之间的进程隔离。
- 作用：设置容器是否与主机或其他容器共享PID命名空间
```shell
# 格式一 --pid="host" 与主机进程共享命名空间
docker run --pid="host" --name="test1" ubuntu
# 格式二 --pid=container:<CONTAINER_NAME>/<ID> 加入其他容器的命名空间
docker run --pid=container:test1 --name="test2" ubuntu
```
> 1. 此功能可用于调试容器内的进程

### 设置容器的UTS Namespace

- UTS Namespace：用来隔离主机名的，每一个UTS Namespace可以拥有一个独立的主机名
- 作用：可以使容器与主机共享UTS Namespace
```shell
# 设置容器与主机共享UTS Namespace
docker run --uts="host" --name="test" ubuntu
# 设置容器的UTS Namespcae
docker run --hostname="<NEW_UTS_NAME>" ubuntu
```
> 1. 若希望容器的主机名随着主机的主机名变化而变化，则可以使用--uts指令。若想设置其他的主机名则使用--hostname指令
> 2. 在使用了--uts指令设置于主机共享UTS后，--hostname和--domainname将会失效

### 设置容器的IPC Namespace

- IPC Namespace：用来隔离进程通信的，可以实现，同一IPC的进程可以通信，不同的IPC的进程不能通信
- 作用：设置容器的IPC模式
```shell
docker run --ipc="<IPC_MODE>" --name="test" ubuntu
```

| **IPC_MODE取值** | **描述** |
| --- | --- |
| "" | 不指定，则使用守护程序的默认值，可配置 |
| "none" | 有私有的IPC空间，但未装入/dev/shm |
| "private" | 有私有的IPC空间，不能与其他容器共享 |
| "shareable" | 有私有的IPC空间，可以与其他容器共享 |
| "container: <_name-or-ID_>" | 加入另一个可共享的容器的IPC命名空间 |
| "host" | 使用主机的IPC命名空间 |

> 1. 当一个程序被分成多个容器时，可使用IPC机制，使主容器设置为shareable，其他容器则使用container: <_name-or-ID_>

## 设置容器的网络
设置容器连接到的网络
```shell
# docker run --network <NETWORL_NAME> <CONTAINER_NAME>
docker run --network host test
```
> 💡 **Note：关于容器网络的更多详情可查看文档：**[**容器网络**](https://www.yuque.com/kongcheng-l8ycr/ci0y0g/ey1bgb9nygk8a9qw#QbQRy)

## 设置容器重启策略
在容器意外停止或退出时，可以给容器设置重启策略，是容器重新启动
```shell
# 指令格式
docker run --restart=<MODE> redis
# 示例
docker run --restart=always redis
docker run --restart=unless-stopped redis
docker run --restart=on-failure:20 redis
```
主要有如下几种策略：

| **MODE取值** | **描述** |
| --- | --- |
| no | 不重启容器，默认策略 |
| on-failure[:max-retries] | 当容器以非0退出状态退出时，重启容器，可以设置重启的次数 |
| always | 始终重启容器，无论docker守护程序启动时，容器的状态是什么，都会重启 |
| unless-stopped | 始终重启容器，除了在docker守护程序停止之前已经停止了的容器 |

> 💡 **Note**
> 1. 若通过`docker stop`或者`docker rm` 删除容器，则重启策略不会生效，换言之，一旦手动停止或删除容器重启策略就会失效
> 2. 每次重启容器时会有一段间隔时间，默认为100ms，每次重启时，间隔时间都是上次重启间隔的两倍，直至达到最大的一分钟间隔，此后便是每隔一分钟启动一次
> 3. 当容器重新启动成功，并且运行至少10秒，则重启间隔时间会重置为100ms
> 4. 可以用指令`docker inspect -f "{{ .RestartCount }}" <CONTAINER_NAME>/<CONTAINER_ID>`查看容器重新启动的次数
> 5. 可以用` docker inspect -f "{{ .State.StartedAt }}" <CONTAINER_NAME>/<CONTAINER_ID>`查看上次容器启动的时间
> 6. `--restart`不能和`--rm`组合使用，会报错

## 设置退出时删除容器
```shell
docker run --rm --name="test" ubuntu
```
> 1. 删除容器时，还会删除与容器关联的匿名卷，仅删除未指定名称的卷
> 2. 类似指令`docker run --rm -v /foo -v awesome:/bar ubuntu top`

## 容器安全配置
```shell
docker run --security-opt="<OPTION>" -it ubuntu
```

| **OPTION** | **描述** |
| --- | --- |
| --security-opt="label=user:USER" | 设置容器的标签用户 |
| --security-opt="label=role:ROLE" | 设置容器的标签角色 |
| --security-opt="label=type:TYPE" | 设置容器的标签类型 |
| --security-opt="label=level:LEVEL" | 设置容器的标签级别 |
| --security-opt="label=disable" | 关闭容器的标签限制 |
| --security-opt="apparmor=PROFILE" | 设置应用于容器的访问控制文件 |
| --security-opt="no-new-privileges:true" | 禁止容器进程获取新权限 |
| --security-opt="seccomp=unconfined" | 关闭容器的seccomp限制 |
| --security-opt="seccomp=profile.json" | 白名单系统调用seccomp Json文件作为seccomp筛选器 |






