## 手搓网站_Week1_Docker

### Docker基本概念

Docker是一个用于开发、配置、运行的开放平台。Docker 将应用与环境相隔离，让应用程序可以得到快速交付。 

• 通俗地讲，Docker是一个虚拟环境容器，可以将你的开发环境、代码、配置文件一并打包放到这个容器中，并发布和应用到任意平台中

**打包**：就是把你软件运行所需的依赖、第三方库、软件打包到一起，变成一个安装包
**分发**：你可以把你打包好的“安装包”上传到一个镜像仓库，其他人可以非常方便的获取和安装
**部署**：拿着“安装包”就可以一个命令运行起来你的应用，自动模拟出一摸一样的运行环境，不管是在 Windows/Mac/Linux。

<img src="E:\Typore-Picture\image-20230329233328894.png" alt="image-20230329233328894" style="zoom: 67%;" />

Docker主要由镜像（image）、容器（container）、仓库（repository）这 三个部分组成 

• 一个类比： • 仓库是大家上传镜像、分享镜像的地方，相当于`github`。docker hub上面有一些 重要的镜像，比如`ubuntu`等。 

• 镜像——类比与C++中的类模板，用于创造容器（container） 

• 容器——类比于C++中的对象，是大家写好的类模板（镜像）的实例化

<img src="E:\Typore-Picture\image-20230329233433883.png" alt="image-20230329233433883" style="zoom:67%;" />

### Docker基本操作

```bash
• docker build <filename> 将源代码打包形成镜像并存放在本地 
• docker pull <filename>: 从docker hub上拉取镜像并存放在本地 
• docker run <filename> : 运行镜像image，如果在本地找到了该镜像就直接启动；否则从docker hub上拉去image并启动 
• 参数-d：后台运行 • 参数-p：端口映射
• docker info: 查看docker信息，如占用空间、版本等 

• docker --help: 获取docker的帮助信息 
• docker <具体命令> --help ：获取docker <具体命令>更 详细的信息 
• docker images: 列出所有本地镜像&详细信息 
• 参数：-a ：列出所有本地镜像，含历史映像层 • 参数：-q ：只显示镜像ID • docker search <filename>: 搜索远程仓库是否有相应的 image

• docker pull <filename>: 拉取镜像
	• example: docker pull centos:latest  #镜像名称和版本号
• docker ps ：查看运行中的容器 
• docker rmi  <filename>： 删除镜像 
		• -f : 如果image正在被停止的容器无法删除，这时加上-f这个参数就 可以被强制删除 
		• example: （删除全部）docker rmi -f $(docker images -qa) 
		• 支持同时删除多个 • docker rm [Options] : 删除容器 
• docker exec [OPTIONS] CONTAINER COMMAND: 进入容器内部进行调试 Docker常用命令

• docker save: 将镜像打包成tar包 
	• example: docker save demo > demo.tar 
• docker load：从tar包加载一个镜像 
	• example: docker load < backend.tar

• docker export 容器ID > 文件名.tar
	• 导出容器内部的内容作为tar归档文件（导出整个容器并进行备份）
• docker import ：将export的容器恢复
```

### 使用`Dockerfile`创造镜像

Dockerfile简介：Dockerfile是用来构建docker镜像 的文本文件。是由一条条构建镜像所需的指令和参数构成的脚本。

 • 使用`Dockerfile`创造镜像的大致流程：

Dockerfile—>docker image —> docker container 

1. 编写`Dockerfile` 
2. docker build ：构建镜像 
3. docker run ： 以镜像为基础构建容

<img src="E:\Typore-Picture\image-20230329234257438.png" alt="image-20230329234257438" style="zoom:67%;" />

<img src="E:\Typore-Picture\image-20230329234318730.png" alt="image-20230329234318730" style="zoom:67%;" />

### Docker: 卷的挂载

```bash
• 命令格式：-v [host-dir]:[container-dir]:[rw|ro]
• example: docker run -it -v /e/demo:/src ubunt
#卷的挂载有什么用？
    • 方便编辑和方便共享
    • 如果有一些数据想在多个容器间共享，或者想在一些临时性的容器中使用该数据，那么最好的方案就是你创建一个数据卷容器，然后从该临时性的容器中挂载该数据卷容器的数据。 这样，即使删除了刚开始的第一个数据卷容器或者中间层的数据卷容器，只要有其他容器使用数据卷，数据卷都不会被删除的。
    • 防止丢失
    • docker rm my_container删除相应的容器时，挂载出来的数据不会丢失
    • 彻底删除使用docker rm -v my_container，避免不必要数据的存在
    • 备份方便
    • 不能使用docker expor t、save、cp等命令来备份数据卷的内容，因为数据卷是存在于镜像之外的。备份的方法可以是创建一个新容器，挂载数据卷容器，同时挂载一个本地目录，然后把远程数据卷容器的数据卷通过备份命令备份到映射的本地目录里面。
```

### 参考资料

[1] `Dockerfile`文档官方教程： https://docs.docker.com/engine/reference/builder/ 

[2] Docker desktop安装：https://docs.docker.com/get-docker/ 

[3] Docker 命令行： https://docs.docker.com/engine/reference/commandline/cli/ 

[4] 卷的挂载 https://blog.csdn.net/fragrant_no1/article/details/83184635
