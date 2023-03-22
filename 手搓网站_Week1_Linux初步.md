## 手搓网站_Week1_Linux初步

### Linux起源

• 1969年，美国 AT&T 公司贝尔实验室开发了 UNIX 操作系统 

• 1983年，理查德·斯托曼在MIT发起了GNU计划(GNU's Not Unix)，并诞生了GPL (通用公共许可协议)

• 1991年，林纳斯·托瓦兹在大学时期编写并发布了Linux内核 

• 随后诞生了许多基于Linux内核的操作系统，称作Linux发行版 • 例如：Debian,Red Hat等分支

### 常用命令

```bash
pwd //显示当前目录
rm a.cpp //删除指定文件
rm -r dir //删除当前文件夹及其下所有文件
mv a.cpp dir/  //将a.cpp文件移动到dir目录下
copy a.cpp dir/ //将a.cpp文件复制到dir目录下
copy -r a/ dir/ //将a目录复制到dir目录下
history //显示历史命令
history -n //显示历史n条命令
whereis file //查找文件所在位置  -m说明文件 -b 二进制文件 -s 源代码文件
whichi ls //查找命令所在位置
>  >>  //覆盖  追加
```

### SSH

SSH(Secure Shell) 是建立在应用层基础上的安全协议，可以用其远程登录服务器/其他电脑

 SSH登录流程

<img src="E:\Typore-Picture\image-20230321223623123.png" alt="image-20230321223623123" style="zoom:80%;" />

本机生成密钥

```bash
ssh-keygen
```

在本机的.ssh/文件夹下![image-20230321223759997](E:\Typore-Picture\image-20230321223759997.png)

`id_rsa`代表着私钥  `id_rsa.pub`代表公钥

将公钥添加到`/home/user/.ssh/authorized_keys` 即可免密登录

```c++
ssh remote_username@remote_address 
remote_username是服务器端用户名  remote_address是服务器地址可以说IP地址或者域名 
```



• 从服务器拷贝到本地 `scp remote_username@remote_address:remote_filename local_folder` 

• 从本地拷贝到服务器 `scp local_file remote_username@remote_address:remote_folder` 

• 对于文件夹需加参数 -r `scp –r local_file remote_username@remote_address:remote_folder`

### 文件权限

<img src="E:\Typore-Picture\image-20230321224341381.png" alt="image-20230321224341381" style="zoom: 50%;" />

<img src="E:\Typore-Picture\image-20230321224358107.png" alt="image-20230321224358107" style="zoom: 50%;" />

```bash
chmod  xxx filename //即可修改权限
```

### tmux

<img src="E:\Typore-Picture\image-20230321231707128.png" alt="image-20230321231707128" style="zoom:67%;" />

若没有tmux就先安装

```bash
sudo apt install tmux //安装tmux
tmux	//打开tmux
Ctrl+B 后输入D  //退出tmux界面

//会话层
tmux new -s <session-name>  //新建会话层并且命名
tmux detach  or Ctrl + B D//分离会话
tmux ls //查看所有会话
tmux attach -t <session-name>  //接入会话
tmux kill -t <session-name>   //杀死会话
tmux switch -t <session-name> //切换会话
tmux <rename-session-name> -t <new-session>  //会话重命名

//窗口层
Ctrl + b  c  //新建窗口
Ctrl + b p/num/n	//切换窗口
Ctrl + “  //上下划分窗口  
Ctrl + %  //左右划分窗口
Ctrl + 上下左右  //切换pane(窗口被划分后叫pane)
```

### 拓展资料

[计算机教育中缺失的一课 · the missing semester of your cs education (missing-semester-cn.github.io)](https://missing-semester-cn.github.io/)

#### 内置命令和外置命令

<img src="E:\Typore-Picture\image-20230321232501094.png" alt="image-20230321232501094" style="zoom:50%;" />

#### 挂起、恢复进程

<img src="E:\Typore-Picture\image-20230321232550321.png" alt="image-20230321232550321" style="zoom:67%;" />

<img src="E:\Typore-Picture\image-20230321232600340.png" alt="image-20230321232600340" style="zoom:67%;" />

