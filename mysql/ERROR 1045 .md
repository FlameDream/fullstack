## ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)



解决ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)：
首先，该问题是提示密码错误，可能是你忘记了密码。此时，可以通过修改配置文件实现免密进入mysql：

具体步骤：

进入 my.cnf文件

cd /etc/mysql

sudo vim my.cnf

# 在socket=/var/lib/mysql/mysql.sock参数下加上：

skip-grant-tables

重启mysql服务：

sudo systemctl stop mysqld.service     #停止服务

sudo systemctl start mysqld.service     #启动服务

登录mysql，输入密码时，直接回车即可进入

mysql -uroot -p

# 输入密码时，直接回车即可

修改密码：(修改配置的方法相当于把你的密码设置为了空，所以你直接回车即可登录，为了确保数据库安全，我们需要修改密码)

update mysql.user set authentication_string='newpassword' where user='root' and host='localhost';

修改成功，下次登录时，输入新密码即可。

