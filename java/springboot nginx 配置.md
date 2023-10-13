安装nginx参考本人另一篇博客：http://www.cnblogs.com/gmq-sh/p/5750833.html

spring-boot需要启动nginx的，用于监听启动的端口。
一、配置nginx：

复制代码
#user  nobody;
worker_processes  1;


#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  testgmq.com; #域名
        index myindex.html;  #指定的server的root的访问页面
        root /home/www/index; #指定的server的root目录

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        #我工程的context-path=mytest
        location /mytest {
                proxy_pass http://localhost:8080;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Port $server_port;
        #    root   html;
        #    index  index.html index.htm;
        }
    }

}
复制代码
 


这里有三点需要说明：
1、nginx允许一个server同时支持http和https两种协议。这里我们分别定义了http:80和https:443两个协议和端口号。如果你不需要http:80则可删除那行。
2、nginx收到请求后将通过http协议转发给tomcat。由于nginx和tomcat在同一台机里因此nginx和tomcat之间无需使用https协议。
3、由于对tomcat而言收到的是普通的http请求，因此当tomcat里的应用发生转向请求时将转向为http而非https，为此我们需要告诉tomcat已被https代理，方法是增加X-Forwared-Proto和X-Forwarded-Port两个HTTP头信息。


二、接着再配置tomcat。基于spring-boot开发时只需在application.properties中进行配置：
server.tomcat.remote_ip_header=x-forwarded-for
server.tomcat.protocol_header=x-forwarded-proto
server.tomcat.port-header=X-Forwarded-Port
server.use-forward-headers=true
该配置将指示tomcat从HTTP头信息中去获取协议信息（而非从HttpServletRequest中获取），同时，如果你的应用还用到了spring-security则也无需再配置。
此外，由于spring-boot足够自动化，你也可以把上面四行变为两行：
server.tomcat.protocol_header=x-forwarded-proto
server.use-forward-headers=true
下面这样写也可以：
server.tomcat.remote_ip_header=x-forwarded-for
server.use-forward-headers=true
但不能只写一行：
server.use-forward-headers=true
具体请参见http://docs.spring.io/spring-boot/docs/1.3.0.RELEASE/reference/htmlsingle/#howto-enable-https，其中说到：
server.tomcat.remote_ip_header=x-forwarded-for
server.tomcat.protocol_header=x-forwarded-proto
The presence of either of those properties will switch on the valve
此外，虽然我们的tomcat被nginx反向代理了，但仍可访问到其8080端口。为此可在application.properties中增加一行：
server.address=127.0.0.1
这样一来其8080端口就只能被本机访问了，其它机器访问不到。

 

 

我是springboot，加了context-path=myproject,但是我绑定的域名又想：www.myxxx.com直径访问我项目中的其中的一个url，所以：

在server_name下面增加了：index，root两个配置。

/home/www/index/myindex.html:

复制代码
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
    <script type="text/javascript">
               <!-- 特定的url作为首页 -->
        window.location.href = "http://www.myxxx.com/myproject/mobile/shopindex.html";
    </script>

</body>
</html>
复制代码
作为跳转的处理。

 

如果有更好的方法，可以互相交流。

