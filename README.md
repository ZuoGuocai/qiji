# 奇技

```
1. 右键---复制ssh渠道，共用一个socket连接，不用输入密码；如果复制ssh渠道为灰色，说明xshell 是Free for Home/School 版本，同一个窗口只能开启4个tab，你关闭一个就行了

xshell中的复制即“复制会话”；复制ssh渠道即“复制socket通道”。
个人理解：
复制会话：需要重新发起连接请求，创建新的线程。
复制通道：共用之前的连接请求，共用之前的线程。



2. -bash: /usr/bin/rm: Argument list too long

find .  -name "metricsdb*"  -exec rm {} \;


只列出目录
ls -d /etc/*/


3.   Linux 上从 NetworkManager 切换为 systemd-network

    docker systemd  cgroup
    
    更改设置，令容器运行时和 kubelet 使用 systemd 作为 cgroup 驱动，以此使系统更为稳定。 请注意在 docker 下设置 native.cgroupdriver=systemd 选项
    https://kubernetes.io/zh/docs/setup/production-environment/container-runtimes/
    
    systemd-cgtop 

    CRI-O(Container Runtime Interface Orchestrator) 是一个轻量级的，专门对Kubernetes 进行优化的容器运行时环境
    
    
4.  -- 停止解析命令行参数

rm -- -mapping.json

```

5. 
```
cat /proc/sys/kernel/random/uuid


```


6.  benchmark


```

sysbench /usr/share/sysbench/oltp_read_write.lua  --table-size=10000 --db-driver=mysql --mysql-host=10.252.4.52 --mysql-port=3306 --mysql-user=root --mysql-password=rootroot --mysql-db=sysbench --threads=10 --tables=10 --events=100000 --time=10 prepare


sysbench /usr/share/sysbench/oltp_read_write.lua  --table-size=10000 --db-driver=mysql --mysql-host=10.252.3.86 --mysql-port=3306 --mysql-user=root --mysql-password=rootroot --mysql-db=sysbench --threads=10 --tables=10 --events=100000 --time=10 run


sysbench /usr/share/sysbench/oltp_read_write.lua  --table-size=10000 --db-driver=mysql --mysql-host=10.252.3.86 --mysql-port=3306 --mysql-user=root --mysql-password=rootroot --mysql-db=sysbench --threads=10 --tables=10 --events=100000 --time=10 --rand-type=uniform cleanup





redis-benchmark -c 50 -n 10000000 -d 10 -k 1 -r 10000 -P 100 -t get
redis-benchmark -c 50 -n 1000000 -d 10 -k 1 -r 10000 -P 1 -t get

redis-benchmark –h 10.252.5.68-c 50 -n 10000000 -d 10 -k 1 -r 10000 -P 100 -t get
redis-benchmark –h 10.252.5.68 -c 50 -n 10000000 -d 10 -k 1 -r 10000 -P 1 -t get

```
