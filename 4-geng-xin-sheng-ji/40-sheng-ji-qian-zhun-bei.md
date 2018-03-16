## 升级注意事项

请先停止运行jumpserver、COCO、guacamole ，然后记得备份哦。

```
ps aux|grep python |awk '{print $2}' |xargs kill -9
```

每一次升级请确保都是成功的，否则访问jumpserver会有各种意外发生，确保每一步都升级成功后请记得清理浏览器缓存。

