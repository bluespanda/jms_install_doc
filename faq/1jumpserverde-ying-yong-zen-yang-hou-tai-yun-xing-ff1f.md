1. jumpserver、coco怎样后台运行?

> 建议使用supervisor,如果觉得麻烦，这里提供一个简单的后台运行命令。
>
> ```
> jumpserver:
> nohup python run_server.py all 2>&1 </dev/null | cat >> log.out &
> coco:
> nohup python run_server.py 2>&1 </dev/null | cat >> log.out &2.
> ```

2. 提示pip: 未找到命令...

> 如果确认安装了pip，那就再确认下是不是安成了pip3,使用pip3 install ... 看一下

1. Windows 无法连接

2. 如果白屏 可能是nginx设置的不对，也可能运行guacamole的docker容器有问题，总之请求到不了guacamole

3. 如果显示没有权限 可能是你在 终端管理里没有接受 guacamole的注册，请接受一下，如果还是不行，就删除刚才的注册，重启guacamole的docker重新注册
4. 如果显示未知问题 可能是你的资产填写的端口不对，或者授权的系统用户的协议不是rdp
5. 创建系统用户时，直接填真实的windows系统帐号信息，并取消自动推送



