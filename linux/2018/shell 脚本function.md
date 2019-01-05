---
layout: page
title: shell 脚本function
permalink: /linux/2018_3_9
---

### shell 脚本function

#### 筛选脚本进程
```
$ ps -u
$ ps -u | grep 'pm2 logs'
$ ps -u | grep 'pm2 logs' | grep -v grep
$ ps -u | grep 'pm2 logs' | grep -v grep | awk '{print $2}'
```

#### while 循环
```
#!/bin/bash  
  
while :
do
	curl http://127.0.0.1:3007/depth/statistics
done 
 
exit 0 
```

#### for 循环
```
#!/bin/bash  
  
step=2 #间隔的秒数，不能大于60  
  
for (( i = 0; i < 60; i=(i+step) )); do  
    curl http://127.0.0.1:3007/depth/statistics >>/data/xxx/auto.log
    sleep $step  
done  
  
exit 0
```

#### 生成脚本命令
```
#!/bin/bash

SERVICE="/data/front/btc_probe.sh"

start(){
    echo "starting..."
    nohup $SERVICE > 'probe.log' 2>&1 &  
    if [ $? -ne 0 ]
    then
        echo "start failed"
        exit $?
    else
        echo $! > $SERVICE.pid 
        echo "start success"
    fi
}
stop(){
    echo "stopping..."
    kill -9 `cat $SERVICE.pid`
    if [ $? -ne 0 ]
    then
        echo "stop failed, may be $SERVICE isn't running"
        exit $?
    else
        rm -rf $SERVICE.pid 
        echo "stop success"
    fi
}
restart(){
    stop
    start
}
status(){
    num=`ps -ef | grep $SERVICE | grep -v grep | wc -l`
    if [ $num -eq 0 ]
    then
        echo "$SERVICE isn't running"
    else
        echo "$SERVICE is running"
    fi
}
case $1 in    
    start)      start ;;  
    stop)      stop ;;  
    restart)  restart ;;
    status)  status ;; 
    *)          echo "Usage: $0 {start|stop|restart|status}" ;;     
esac  

exit 0
```