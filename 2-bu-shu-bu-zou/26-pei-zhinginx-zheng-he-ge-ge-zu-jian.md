## 配置Nginx整合各个组件

###  安装nginx（根据喜好选择安装方式和版本）

> 系统自带的nginx版本比较低，这里提供yum安装最新稳定版的步骤。若想编译安装，请自行查阅文档。

####  新增nginx repo仓库地址

```
echo '[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1'  > /etc/yum.repos.d/nginx.repo
```

####  安装nginx

```
sudo yum install  nginx  -y 
```

#### 修改配置文件 

修改nginx 配置文件，vi /etc/nginx/nginx.conf

```
server {
    listen 80;

    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

    location /luna/ {
        try_files $uri / /index.html;
        alias /opt/luna/;
    }

    location /media/ {
        add_header Content-Encoding gzip;
        root /opt/jumpserver/data/;
    }

    location /static/ {
        root /opt/jumpserver/data/;
    }

    location /socket.io/ {
        proxy_pass       http://localhost:5000/socket.io/;
        proxy_buffering off;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    location /guacamole/ {
        proxy_pass       http://localhost:8181/;
        proxy_buffering off;
        proxy_http_version 1.1;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $http_connection;
        access_log off;
    }

    location / {
        proxy_pass http://localhost:8080;
    }
}
```

#### 检查配置并启动

```
nginx  -t
systemctl enable nginx
systemctl start nginx
```

#### 防火墙开启端口

若是云服务器还需要单独在其安全策略上放行80端口（没备案的请改其他端口），公网才能访问。

```
sudo firewall-cmd --zone=public --add-port=80/tcp --permanent
sudo firewall-cmd  --reload
```

#### 登录jumpserver

登录junmpserver，使用各个功能模块是否都正常。



