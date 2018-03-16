## 升级guacamole

```
$ docker pull registry.jumpserver.org/public/guacamole:latest
$ docker stop jms_guacamole  # 或者写guacamole的容器ID
$ docker run --name jms_guacamole -d \
  -p 8081:8080 -v /opt/guacamole/key:/config/guacamole/key \
  -e JUMPSERVER_KEY_DIR=/config/guacamole/key \
  -e JUMPSERVER_SERVER=http://<填写本机的IP地址>:8080 \
  registry.jumpserver.org/public/guacamole:latest
```



