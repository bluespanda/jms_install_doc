jumpserver、coco怎样后台运行?

> 建议使用supervisor,如果觉得麻烦，这里提供一个简单的后台运行命令。
>
> ```
> jumpserver:
> nohup python run_server.py all 2>&1 </dev/null | cat >> log.out &
> coco:
> nohup python run_server.py 2>&1 </dev/null | cat >> log.out &
> ```

提示pip: 未找到命令...

> 如果确认安装了pip，那就再确认下是不是安成了pip3,使用pip3 install ... 看一下

Windows 无法连接

> * 如果白屏 可能是nginx设置的不对，也可能运行guacamole的docker容器有问题，总之请求到不了guacamole
> * 如果显示没有权限 可能是你在 终端管理里没有接受 guacamole的注册，请接受一下，如果还是不行，就删除刚才的注册，重启guacamole的docker重新注册
> * 如果显示未知问题 可能是你的资产填写的端口不对，或者授权的系统用户的协议不是rdp
> * 创建系统用户时，直接填真实的windows系统帐号信息，并取消自动推送

coco或guacamole 注册失败，或重新注册方法

> ```
> (1). 停止 coco 或 删掉guacamole的docker
>    $ kill <coco的pid>
>    $ docker rm -f <guacamole docker的id>
> (2). 在 Jumpserver后台 会话管理 - 终端管理  删掉它们
> (3). 删掉它们曾经注册的key
>    $ rm keys/.access_key  # coco
>    $ rm /opt/guacamole/key/*  # guacamole, 如果你是按文档安装的，key应该在这里
> ```

input/output error, 通常jumpserver所在服务器字符集问题\(一下修改方法仅限 centos7\)

> ```
> $ localedef -c -f UTF-8 -i zh_CN zh_CN.UTF-8
> ```
>
> ```
> $ export LC_ALL=zh_CN.UTF-8
> $ echo 'LANG=zh_CN.UTF-8' > /etc/sysconfig/i18n
> ```



