### 时间服务器搭建
```
docker run --restart=always --privileged -itd --cap-add SYS_TIME --name ntp --publish 123:123/udp alvistack/chrony-3.5
```

### 客户端检查本地是否有ntp服务器，如果有就删掉

```
ntpdate 127.0.0.1
```

