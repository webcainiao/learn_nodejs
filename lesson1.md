# 学习nodejs前后端开发的一些基础设置

标签（）： web 

---
##电脑操作系统的选择
> * 推荐选用linux做程序运行平台，云主机，本人使用centos发行版，需要了解一些linux基础知识，推荐 [`linux就该这么学`](http://www.linuxprobe.com/)。
* windows平台，上边装个linux虚拟机，可以在windows下编辑代码，linux运行代码

##增加一个linux用户，使用sudo可不显示密码
> \# useradd username
\# passwd username
\# visudo
更改打开的文件，里面添加一行:（打开了/etc/sudoers）
username ALL=(ALL) NOPASSWD:ALL
然后,
\# su username //切换用户
\$ sudo -k //清空安全时间？


##linux改变yum源为阿里云，提高下载，安装速度<http://mirrors.aliyun.com/help/centos>
```
1. 备份 mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
2. 下载新的CentOS-Base.repo 到/etc/yum.repos.d/
CentOS 5
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
CentOS 6
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
CentOS 7
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
3、之后运行yum makecache生成缓存
```

##安装gcc gcc-c++,供源码编译
```
$ yum list | grep gcc //查询yum库中的包
$ rpm -q gcc //查询是否安装
$ yum -y install gcc //yum安装
```

##安装nvm
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
```
注意版本号，然后在用户目录下，查看是否有,.bash_profile  .zshrc  .profile  .bashrc等目录，我的有.bashrc，在其中添加：
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```
注意\$HOME的使用，然后，
```
$ source ~/.bashrc  //使上边代码生效
$ nvm //安装成功会有提示
$ nvm install xxxxx
$ nvm alias xxxxx //指定默认版本
```
## 安装nrm,切换npm源
```
$ npm install -g nrm
$ nrm ls
$ nrm use xxx
```
##安装git
可用yum或自行编译安装

* 和github关联
    > $ ssh-keygen -t rsa -C "youremail"
在用户目录下生成，.ssh目录，含有id_rsa,id_rsa.pub文件，将id_rsa.pub的内容，添加到github的SSH keys中。

* 设置当前用户下推送的git使用者
```
$ git config --global user.name "yourname" 
$ git config --global user.email "email"
```
信息保存在~/.gitconfig中,若不设置，commit到github上的信息，显示不出是谁推送的。

*推送和拉取
> 如：本地有git库a目录，github有空库b库。执行：

```
$ cd /a/
$ git remote add origin git@github.com:yourname/b.git
```
将a,b库关联，执行：
```
$ git push -u origin master
```
clone/pull/push等命令会有一些提示，不必在意，确认即可。此命令，第一次执行，加上`-u`参数，则本地master分支就推送到远程b库的master了,之后可简化命令：
```
$ git push/pull
```
取消本地和远程库关联：
```
$ git remote remove origin
```

* 可从github直接clone项目
    > git clone git@github:yourname/xxx.git
cd xxx //进入该目录，进行后续操作

***
以上完成后，就可以将写好的代码，使用：
```
$ node xxxxxx  //执行代码
```
若要建立稍复杂项目，需要使用：yeoman react webpack 等开发工具，使用nginx作为web代理服务器，反向代理，负载均衡等。
使用xftp,winscp等上传工具.....
