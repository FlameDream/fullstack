# no input files specified的解决方法


在开发新项目，配置的时候遇到No input file specified.的问题。No input file specified.（没有指定输入文件）从字面意思看一看出，可能是服务器配置问题，或者是文件不存在等问题。

### 具体解决方案如下：

**1.检查服务器配置路径是否指对（或者是所指文件是否存在）**

**2.检查指向的文件是否允许访问**

**3.检查服务器配置是否正确（服务器的配置项都是从A拷贝到B，在修改个别配置）**


例如：

之前配置了一个TP框架的nginx配置，但是后来把前后端分离，这个配置项就比较尴尬了（No input file specified.）


```bash
server
        {
                listen 80;
                #listen [::]:80;
                server_name xxxxx.com;
                index index.html index.htm index.php default.html default.htm default.php;
                root /var/www/xxxx/;

        #       try_files $uri  /index.php/$uri;

	        location ~ .*\.php($|/)
	        {
	           fastcgi_pass  unix:/tmp/php-cgi.sock;
	           fastcgi_index index.php;
	           fastcgi_split_path_info ^(.+\.php)(/.*)$;
	           fastcgi_param PATH_INFO $fastcgi_path_info;
	           include fastcgi.conf;
	        }

	        location / {
	                try_files  $uri  /index.php$uri;
	         }

                location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
                {
                        expires      30d;
                }

                location ~ .*\.(js|css)?$
                {
                        expires      12h;
                }
        }
```

修改后

```bash
server
        {
                listen 80;
                #listen [::]:80;
                server_name xxxxx.com;
                index index.html index.htm index.php default.html default.htm default.php;
                root /var/www/xxxx/;

       
	        location / {
	                  index index.html;
	         	}

                location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
                {
                        expires      30d;
                }

                location ~ .*\.(js|css)?$
                {
                        expires      12h;
                }
        }

```


最终问题解决。






