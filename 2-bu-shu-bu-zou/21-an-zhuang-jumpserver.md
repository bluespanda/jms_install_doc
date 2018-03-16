## 安装 jumpserver

### 下载或 Clone 项目 {#221下载或-clone-项目}

> 因为网络等其他原因，git clone可能比较慢，也可以选择去[Github](https://github.com/jumpserver/jumpserver)上直接下载zip包。

```
$ cd /opt/
$ sudo git clone --depth=1 https://github.com/jumpserver/jumpserver.git && cd jumpserver && git checkout master
```

### 安装依赖 RPM 包

```
$ cd /opt/jumpserver/requirements
$ sudo yum -y install $(cat rpm_requirements.txt)
```

> 如果没有任何报错请继续,有错就想法解决掉错误！

### 安装 Python 库依赖

```
$ sudo pip install -r requirements.txt
```

> 不要指定-i参数，因为镜像上可能没有最新的包，如果没有任何报错请继续

### 修改 Jumpserver 配置文件

```
$ cd /opt/jumpserver
$ sudo cp config_example.py config.py
$ sudo vi config.py
```

> 注意: 配置文件是 Python 格式，不要用 TAB，而要用空格&lt;br&gt;

根据自己的需求更改IP地址、数据库相关信息

```
class DevelopmentConfig(Config):
```

```
DEBUG = True

DB\_ENGINE = 'mysql'

DB\_HOST = '127.0.0.1'

DB\_PORT = 3306

DB\_USER = 'jumpserver'

DB\_PASSWORD = 'somepassword'

DB\_NAME = 'jumpserver'
...
config = DevelopmentConfig\(\)  \# 确保使用的是刚才设置的配置文件
```

### 生成数据库表结构和初始化数据

```
$ cd /opt/jumpserver/utils
$ sudo bash make_migrations.sh
```

### 防火墙开启8080端口

> 开放8080端口

```
sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent
```

> 载入配置生效

```
sudo firewall-cmd --reload
```

### 关闭selinux

```
$ sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
$ sudo setenforce 0
```

### 运行 Jumpserver

```
$ cd /opt/jumpserver
$ sudo python run_server.py all
# 如果需要后台运行请查看QFA章节
```

运行不报错，请浏览器访问 [http://IP地址:8080/](http://IP地址:8080/) \(这里只是 Jumpserver, 没有 Web Terminal，所以访问 WEB终端 会报错\)

> 默认帐号及密码：admin



