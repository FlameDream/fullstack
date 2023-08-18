
# Nginx常用命令


在Nginx服务器配置过程中，大致可以把Nginx的命令分为两块：

	一块是Nginx的命令行命令，主要用来查看Nginx的安装信息，帮助信息等。
	一块是Nginx的运维命令，主要用来服务的启动、重启和停止等。


### 命令行命令

Nginx的命令行参数比较少，我们可以使用以下命令查看Nginx支持的命令：

```bash

Usage: nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives]

Options:
  -?,-h         : this help
  -v            : show version and exit
  -V            : show version and configure options then exit
  -t            : test configuration and exit
  -T            : test configuration, dump it and exit
  -q            : suppress non-error messages during configuration testing
  -s signal     : send signal to a master process: stop, quit, reopen, reload
  -p prefix     : set prefix path (default: /usr/local/nginx/)
  -c filename   : set configuration file (default: conf/nginx.conf)
  -g directives : set global directives out of configuration file


  #下面分别对这些参数做下说明  

  	nginx -h：查看帮助
	nginx -v：查看nginx的版本
	nginx -V：查看版本和nginx的配置选项
	nginx -t：测试配置文件的正确性
	Nginx -T: 测试配置文件，并显示配置文件（这个命令可以快速查看配置文件）
	nginx -q：测试配置文件，但是只显示错误信息
	nginx -s：发送信号，下面详细介绍
	nginx -p：设置前缀
	nginx -c：设置配置文件
	nginx -g：附加配置文件路径

```

### 运维命令

运维命令常用命令主要用于对Nginx服务的启动、重启和停止等。


```bash

nginx -t   # 检查当前nginx配置状态

nginx -s reload   # 重新加载Nignx

nginx -s reopen  # 用来完成新日志的生成


nginx -s stop       #快速关闭Nginx，可能不保存相关信息，并迅速终止web服务。
nginx -s quit       #平稳关闭Nginx，保存相关信息，有安排的结束web服务。
nginx -s reload    	#因改变了Nginx相关配置，需要重新加载配置而重载。
nginx -s reopen     #重新打开日志文件。
nginx -c filename   #为 Nginx 指定一个配置文件，来代替缺省的。
nginx -t            #不运行，仅仅测试配置文件。nginx 将检查配置文件的语法的正确性，并尝试打开配置文件中所引用到的文件。
nginx -v            #显示 nginx 的版本。
nginx -V            #显示 nginx 的版本，编译器版本和配置参数。

```





