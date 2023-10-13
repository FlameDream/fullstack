查看端口的使用的情况

lsof 命令
1
比如查看80端口的使用的情况。

lsof -i tcp:80

列出所有的端口

netstat -ntlp


netstat -nupl (UDP类型的端口)
netstat -ntpl (TCP类型的端口)

 

a 表示所有

n表示不查询dns

t表示tcp协议

u表示udp协议

p表示查询占用的程序

l表示查询正在监听的程序

 

netstat -nuplf|grep 3306   //这个表示查找处于监听状态的，端口号为3306的进程



        前提：首先你必须知道，端口不是独立存在的，它是依附于进程的。某个进程开启，那么它对应的端口就开启了，进程关闭，则该端口也就关闭了。下次若某个进程再次开启，则相应的端口也再次开启。而不要纯粹的理解为关闭掉某个端口，不过可以禁用某个端口。

 

1. 可以通过"netstat -anp" 来查看哪些端口被打开。

（注：加参数'-n'会将应用程序转为端口显示，即数字格式的地址，如：nfs->2049, ftp->21，因此可以开启两个终端，一一对应一下程序所对应的端口号）

 

2. 然后可以通过"lsof -i:$PORT"查看应用该端口的程序（$PORT指对应的端口号）。或者你也可以查看文件/etc/services，从里面可以找出端口所对应的服务。

（注：有些端口通过netstat查不出来，更可靠的方法是"sudo nmap -sT -O localhost"）

 

3. 若要关闭某个端口，则可以：

1)通过iptables工具将该端口禁掉，如：

"sudo iptables -A INPUT -p tcp --dport $PORT -j DROP"

"sudo iptables -A OUTPUT -p tcp --dport $PORT -j DROP"   

2)或者关掉对应的应用程序，则端口就自然关闭了，如：

"kill -9 PID" (PID：进程号)

如：    通过"netstat -anp | grep ssh"

有显示：    tcp 0 127.0.0.1:2121 0.0.0.0:* LISTEN 7546/ssh

则：    "kill -9 7546"



查看端口的状态

 /etc/init.d/iptables status

开启端口
开启端口以开启端口80为例。
1 用命令开启端口：

iptables -I INPUT -p tcp --dport 80 -j accpet --写入要开放的端口
/etc/init.d/iptables save --保存修改
/etc/sysconfig/iptables restart -- 重启防火墙
或者用命令:service iptables restart重启防火墙
1
2
3
4
2 修改/etc/sysconfig/iptables文件。

保存文件重启防火墙。
关闭端口
用命令修改

iptables -I INPUT -p tcp --dport 80 -j DROP--写入修改
/etc/init.d/iptables save --保存修改
service iptables restart --重启防火墙
1
2
3
修改配置文件 vi /etc/sysconfig/iptables：

 -A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j DROP   重启防火墙，修改完成



 在 Linux 中，您可以使用命令行工具来查看本机上已经开放的端口。具体的方法如下：

打开终端，进入命令行环境。

输入命令：netstat -tln。

按下回车键，等待命令执行结果。

在命令输出中，您会看到所有已经在本机上开放的端口及其状态。其中，“t”表示TCP协议，“l”表示监听状态，“n”表示端口号使用数字表示。

例如，如果您想查看端口 80 的状态，您可以使用以下命令：

netstat -tln | grep 80

其中，“| grep”是一个管道符，它将命令的输出传递给另一个命令。在这个例子中，我们将 netstat 命令的输出传递给 grep 命令，然后使用“80”作为过滤条件。这将只显示与端口 80 相关的输出。

请注意，在某些系统中，您可能需要以 root 用户身份运行这些命令，才能查看所有的端口信息。


https://blog.csdn.net/ljbmxsm/article/details/50650008
https://blog.csdn.net/chen3888015/article/details/81095895