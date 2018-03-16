## 安装windows支持组件

因为手动安装 guacamole 组件比较复杂，所以建议直接使用打包好的 guacamole docker镜像 。

### 安装Docker CE

#### 卸载旧版本

> Docker 的早期版本称为 docker 或 docker-engine。如果安装了这些版本，请卸载它们及关联的依赖资源。

```
$ sudo yum remove docker \
                  docker-common \
                  docker-selinux \
                  docker-engine
```

如果 yum 报告未安装任何这些软件包，这表示情况正常。

#### 使用镜像仓库进行安装

```
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
$ sudo yum-config-manager \
     --add-repo \
     https://download.docker.com/linux/centos/docker-ce.repo
$ sudo yum makecache fast
$ sudo yum install docker-ce
```

#### 启动docker

```
 sudo systemctl enable docker
 sudo systemctl start docker
```

#### 下载并运行guacamole

> 注意：这里面的IP地址要改成junmpserver所在服务器的IP地址, 否则会出错。下次耗时较长请安排好时间。

```
docker run -d \
  -p 8181:8080 -v /opt/guacamole/key:/config/guacamole/key \
  -e JUMPSERVER_KEY_DIR=/config/guacamole/key \
  -e JUMPSERVER_SERVER=http://<填写本机的IP地址>:8080 \
  registry.jumpserver.org/public/guacamole:1.0.0
```

> 这里所需要注意的是 guacamole 暴露出来的端口是 8181，若与主机上其他端口冲突请自定义一下。

#### 防火墙开启端口

> 开放8181端口

```
sudo firewall-cmd --zone=public --add-port=8181/tcp --permanent
```

> 载入配置生效

```
sudo firewall-cmd --reload
```

#### 注册终端

一定要记得修改 JUMPSERVER\_SERVER 环境变量的配置，填上 Jumpserver 的内网地址, 然后在guacamole 都跑起来后，这时去 

```
Jumpserver平台-会话管理-终端管理
```

接受\[Gua\]开头的一个终端注册。稍等几秒就可以看到激活中和在线都是绿色的了。

