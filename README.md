# 奇技

```
1. 右键---复制ssh渠道，共用一个socket连接，不用输入密码；如果复制ssh渠道为灰色，说明xshell 是Free for Home/School 版本，同一个窗口只能开启4个tab，你关闭一个就行了

xshell中的复制即“复制会话”；复制ssh渠道即“复制socket通道”。
个人理解：
复制会话：需要重新发起连接请求，创建新的线程。
复制通道：共用之前的连接请求，共用之前的线程。



2. -bash: /usr/bin/rm: Argument list too long

find .  -name "metricsdb*"  -exec rm {} \;


3.   Linux 上从 NetworkManager 切换为 systemd-network

    docker systemd  cgroup
    
    更改设置，令容器运行时和 kubelet 使用 systemd 作为 cgroup 驱动，以此使系统更为稳定。 请注意在 docker 下设置 native.cgroupdriver=systemd 选项
    https://kubernetes.io/zh/docs/setup/production-environment/container-runtimes/

```
