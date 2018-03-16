## 启动所有应用

> 记得切换python虚拟环境

切换python虚拟环境

```
source /opt/py3/bin/activate
```

启动jumpserver

**例：\(py3\) \[ops@monitor ~\]$ cd /opt/jumpserver 注意环境**

```
cd /opt/jumpserver
nohup python run_server.py all 2>&1 </dev/null | cat >> log.out &
```

启动coco（注意环境）

```
nohup python run_server.py 2>&1 </dev/null | cat >> log.out &
```



