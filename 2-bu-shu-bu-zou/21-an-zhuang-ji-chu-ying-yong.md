### 安装第三方仓库 {#211-安装第三方仓库}

```
sudo yum install -y epel-release
```

### 安装基础依赖 {#212-安装各种依赖}

```
sudo yum -y install  wget sqlite-devel xz gcc automake zlib-devel openssl-devel
```

### 安装git工具 {#213-安装git工具}

```
sudo yum install  git -y
```

### 安装Python3 和 Python 虚拟环境 {#214-安装python3-和-python-虚拟环境}

> 编译安装

```
# wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tar.xz
# tar xvf Python-3.6.1.tar.xz  && cd Python-3.6.1
# ./configure &&make && make install
```

#### 建立 Python 虚拟环境 {#2142-建立-python-虚拟环境}

> 因为 CentOS 6/7 自带的是 Python2，而 Yum 等工具依赖原来的 Python，为了不扰乱原来的环境所以我们使用 Python 虚拟环境。

```
# cd /opt
# python3 -m venv py3
# source /opt/py3/bin/activate
```

> 看到下面的提示符\(py3\)代表成功，以后运行 Jumpserver 都要先运 source /opt/py3/bin/activate 命令，jumpserver的所有命令均在该虚拟环境中运行

```
(py3) [root@localhost py3]
```

## 安装redis {#215-安装redis}

> Jumpserver 使用 Redis 做 cache 和 celery broke
>
> yum安装redis

```
sudo yum installredis -y
```

> 开机启动redis

```
sudo systemctl enable redis
```

> 启动redis

```
sudo systemctl startredis
```

## mariadb {#216-mariadb}

> 安装mariadb

```
sudo yum -y install mariadb mariadb-devel mariadb-server
```

> 设置开机启动

```
 sudo systemctl enablemariadb
```

> 启动mariadb

```
 sudo systemctl start  mariadb
```

### 初始化mariadb数据库 {#2161-初始化mariadb数据库}

> 执行命令，根据提示进行初始化

```
# mysql_secure_installation
```

> 初始化内容如下：

```
Enter current password for root (enter fornone):<–初次运行直接回车
Set root password? [Y] <–是否设置root用户密码，输入y并回车或直接回车
New password: <–设置root用户的密码
Re-enter new password: <–再输入一次你设置的密码
Remove anonymous users? [Y] <–是否删除匿名用户，回车
Disallow root login remotely? [Y/n] <–是否禁止root远程登录,回车
Remove test database andaccess to it? [Y] <–是否删除test数据库，回车
Reload privilege tables now? [Y/n] <–是否重新加载权限表，回车初始化MariaDB
完成，接下来测试登录
$ sudo mysql -u root -p
#输入您的密码
```

### 2.1.6.2 创建数据库 Jumpserver 并授权 {#2162-创建数据库-jumpserver-并授权}

> 登录mariadb后执行

```
mysql -u root -p
> create database jumpserver default charset 'utf8'
> grant all on jumpserver.* to 'jumpserver'@'127.0.0.1' identified by 'somepassword';
```



