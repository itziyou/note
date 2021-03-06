[TOC]

# Docker学习笔记

## 1、Docker简介

### 是什么

| 为什么会有docker出现？                                       |
| ------------------------------------------------------------ |
| 一款产品从开发到上线，从操作系统到运行环境，再到应用配置。作为开发+运维之间的协作我们需要关心很多东西，特别是各种版本的迭代之后，不同版本环境的兼容，对运维人员都是一种考验。环境配置如此麻烦，换一台机器，就要重来一次，费时费力。<br/>Docker之所以发展迅速，也是因为它对此给出了一个标准化的解决方案。开发人员利用Docker可以消除协作编码时“在我的机器上可以正常工作”的问题。Docker镜像的设计，**使得Docker可以打破过去“程序即应用”的观念。透过镜像（images）将作业系统核心除外，运行应用程序所需要的的系统环境，由下而上打包，达到应用程序跨平台间的无缝衔接。** |

| Docker理念                                                   |
| ------------------------------------------------------------ |
| Docker是基于Go语言实现的云开源项目。<br/>Docker的主要目标是“Build，Ship and Run Any App，Anywhere”，也就是通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的APP（可以是一个WEB应用或数据库应用等等）及其运行环境能够做到“**一次封装，到处运行**”。<br/>Linux容器技术的出现就解决了这样一个问题，而Docker就是在它的基础上发展过来的。将应用运行在Docker容器上面，而Docker容器在任何操作系统上都是一致的，这就实现了跨平台、跨服务器。**只需要一次配置好环境，换到别的机子上就可以一键部署，大大简化了操作** |

| 一句话                                                       |
| ------------------------------------------------------------ |
| 解决了运行环境和配置问题，方便做持续集成并有助于整体发布的容器虚拟化技术。 |

### 能干嘛

| 虚拟机技术                                                   |
| ------------------------------------------------------------ |
| 虚拟机（virtual machine）就是带环境安装的解决方案。它可以在一种操作系统里边运行另一种操作系统。对于底层系统来说，虚拟机就是一个普通文件，不需要了就删除，对其他部分毫无影响。<br/>虚拟机的缺点：1、资源占用多  2、冗余步骤多  3、启动慢 |

| 容器虚拟化技术                                               |
| ------------------------------------------------------------ |
| 由于前面虚拟机存在的缺点，Linux发展出了另一种虚拟机化技术：Linux容器（Linux Containers，缩写为LXC）。<br/>**Linux容器不是模拟一个完整的操作系统**，而是对进程进行隔离。有了容器，就可以将软件运行所需的所有资源打包到一个隔离的容器中。容器和虚拟机不同，不需要捆绑一套操作系统，只需要软件工作所需的库资源和设置。系统因此而变得高效轻量并保证部署在任何环境中的软件都能始终如一地运行。<br/>Docker和传统虚拟化方式的不同之处：<br/>1、传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整的操作系统，在该系统上在运行所需应用进程<br>2、容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核，**而且也没有进行硬件虚拟**。因此容器比传统虚拟机更为轻便<br/>3、每个容器之间相互隔离，每个容器有自己的文件系统，容器之间进程不会相互影响，能区分计算资源。 |

| 开发/运维（DevOps）    | 一次构建、到处运行                                           |
| ---------------------- | ------------------------------------------------------------ |
| 更快速的应用交付与部署 | 传统的应用开发完成后，需要提供一堆安装程序和配置说明文档，安装部署后需根据配置文档进行繁杂的配置才能正常运行。Docker化之后只需要交付少量容器镜像文件，在正式生产环境加载镜像并运行即可，应用安装配置在镜像里已经内置好，大大节省部署配置和测试验证的时间 |
| 更便捷的升级和扩容     | 随着微服务架构和Docker的发展，大量的应用会通过微服务方式架构，应用的开发构建将变成搭积木一样，每个Docker容器将变成一块“积木”，应用的升级将变得非常容易。当现有的容器不足以支撑业务处理时，可通过镜像运行新的容器进行快速扩容，使应用系统的扩容从原来的天级变成分钟级甚至秒级 |
| 更简单的系统运维       | 应用容器化运行后，生产环境运行的应用与开发、测试环境的应用高度一致，不会因为底层基础架构和构建系统的不一致性给应用带来影响。产生新的BUG，当出现程序异常时，也可以通过测试环境的想通的容器进行快速定位和修复 |
| 更高效的计算资源利用   | Docker是内核级虚拟化，其不像传统的虚拟化技术一样需要额外的Hypervisor支持，所以在一台物理机上可以运行很多个容器实例，可大大提升物理服务器的CPU和内存的利用率 |



### 去哪下

Docker官网：https://www.docker.com/

Docker Hub官网：https://hub.docker.com/

## 2、Docker安装

### CentOS7 安装

**官方文档**：https://docs.docker.com/engine/install/centos/

1、安装需要的软件包

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
```

2、设置stable镜像仓库

```shell
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

3、更新yum软件包索引

```shell
yum makecache fast
```

4、安装docker-ce

```shell
 yum -y install docker-ce
```

5、启动docker

```shell
systemctl start docker
```

6、查看docker版本

```shell
docker version
```

7、拉取并运行hello-world

```shell
docker pull hello-world

docker pull hello-world
```

8、配置阿里云镜像加速 https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors

```shell
# 创建目录
mkdir -p /etc/docker

# 修改配置文件
vim  /etc/docker/daemon.json
{
  "registry-mirrors": ["https://｛自已的编码｝.mirror.aliyuncs.com"]
}

# 重新加载
systemctl daemon-reload

# 重启docker
systemctl restart docker

```



### Windows安装

**安装要求：**

- Windows 10 64位：专业版，企业版或教育版（内部版本15063或更高版本）。
- 必须启用Hyper-V和Containers Windows功能。
- 要在Windows 10上成功运行Client Hyper-V，需要满足以下硬件先决条件：
  - 具有二级地址转换（SLAT）的 64位处理器
  - 4GB系统内存
  - 必须在BIOS设置中启用BIOS级硬件虚拟化支持。

**文件下载**：https://hub.docker.com/editions/community/docker-ce-desktop-windows/



## 3、Docker常用命令

**帮助命令**

```shell
docker version

docker info

docker --help
```

**镜像命令**

docker images    列出本主机上的镜像

![](https://github.com/itziyou/note/blob/master/img/docker/docker_001.png)

## 4、Docker镜像

## 5、容器间通信

## 6、Docker容器数据卷

## 7、DockerFile解析

## 8、Docker常用安装

## 9、Docker Compose

## 10、本地镜像发布到阿里云

