## 安装COCO

> 在安装COCO前，确保jumpserver启动正常，然后重新打开一个ssh 终端，jumpserver若已经后台运行了则不影响

### 下载或 Clone 项目

```
$ cd /opt
$ sudo git clone https://github.com/jumpserver/coco.git && cd coco && git checkout mast
```

### 安装依赖

```
$ cd /opt/coco/requirements
$ yum -y  install $(cat rpm_requirements.txt)
$ sudo pip install -r requirements.txt
```

### 配置COCO

```
$ cd /opt/coco
$ sudo cp conf_example.py conf.py
```

根据自己的需求来更改参数，下面为例子：

```
# 项目名称, 会用来向Jumpserver注册, 识别而已, 不能重复
    # NAME = "monitor"
    # Jumpserver项目的url, api请求注册会使用
    # CORE_HOST = os.environ.get("CORE_HOST") or 'http://192.168.200.101:8080'
    # 启动时绑定的ip, 默认 0.0.0.0
    # BIND_HOST = '0.0.0.0'
    # 监听的SSH端口号, 默认2222
    # SSHD_PORT = 2222
    # 监听的HTTP/WS端口号，默认5000
    # HTTPD_PORT = 5000
```

### 运行COCO

```
$ sudo python run_server.py
```



