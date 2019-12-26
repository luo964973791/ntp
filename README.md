### 时间服务器搭建

```
yum install ntpdate -y && ntpdate ntp1.aliyun.com && hwclock --systohc
```

### 创建docker挂载文件，vi /etc/ntpd.conf

```
vi /data/ntpd.conf
# See ntpd.conf(5) and /etc/examples/ntpd.conf

listen on *

server ntp1.aliyun.com
server ntp2.aliyun.com
```

### 再次确认硬件时钟服务器。

```
ntpdate ntp1.aliyun.com && hwclock --systohc
```

### 启动时间服务器,要等待十分钟才能在客户端同步，要注意。

```
docker run --name=ntp --restart=always --detach=true --publish=123:123/udp --cap-add=SYS_NICE --cap-add=SYS_RESOURCE --cap-add=SYS_TIME -v /data/ntpd.conf:/etc/ntpd.conf cturra/ntp
```

### 客户端检查本地是否有ntp服务器，如果有就删掉

```
lsof -i:123
kill -9 `lsof -i:123 | grep "*:ntp" | awk '{print $2}'`
```

