### docker和虚拟机

![image-20200909210846133](/home/qinh1/.config/Typora/typora-user-images/image-20200909210846133.png)

### docker的组成

Docker由镜像(image)、容器(container)、仓库(repository)组成

* 镜像(image)

  系统盘，包含系统和必备的软件，可以使用docker images来查询

  ![image-20200909211148724](/home/qinh1/.config/Typora/typora-user-images/image-20200909211148724.png)

  上述名称含义如下：

  * REPOSITORY：仓库名称
  * TAG： 镜像标签，其中 lastest 表示最新版本
  * IMAGE ID ：镜像唯一ID
  * CREATED ：创建时间
  * SIZE ：镜像大小

* 容器(container)

  容器可以理解成一个linux的电脑，可以直接运行，是跑项目程序、消耗机器资源，提供服务的东西。容器是基于镜像启动的，可以使用`docker ps -a`来查看存在的容器。

  ![image-20200909211553860](/home/qinh1/.config/Typora/typora-user-images/image-20200909211553860.png)

* 仓库(repository)

  仓库用来存放镜像的，类似于git，可以从中心仓库下载镜像，也可以从自建仓库下载，仓库分为公开仓库和私有仓库。

### Docker促使开发流程变更

![img](https://user-gold-cdn.xitu.io/2019/4/9/16a02cdab4959cfc?imageslim)

![img](https://user-gold-cdn.xitu.io/2019/4/9/16a02cdab5b3597f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### docker的常用命令


