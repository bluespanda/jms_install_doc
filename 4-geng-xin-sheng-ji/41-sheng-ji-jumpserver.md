## 开始升级

### 升级 Jumpserver

```
$ git pull && pip install -r requirements/requirements.txt && cd utils && sh make_migrations.sh
```

### 升级 COCO

```
$ git pull && cd requirements &&  pip install -r requirements.txt   # 不要指定 -i参数
```

### 升级 luna

重新下载 release 包,[https://github.com/jumpserver/luna/releases](https://github.com/jumpserver/luna/releases)

### 升级guacamole

```
$ docker pull registry.jumpserver.org/public/guacamole:latest
$ docker stop jms_guacamole  # 或者写guacamole的容器ID
$ docker run --name jms_guacamole -d \
  -p 8081:8080 -v /opt/guacamole/key:/config/guacamole/key \
  -e JUMPSERVER_KEY_DIR=/config/guacamole/key \
  -e JUMPSERVER_SERVER=http://<填写本机的IP地址>:8080 \
  registry.jumpserver.org/public/guacamole:latest
```



