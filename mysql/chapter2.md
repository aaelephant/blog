
#mysql 5.7.22 linux generic 版本安装

####系统环境 aliyunlinux server release 17.01.2

1. 下载 mysql-5.7.22-linux-glibc2.12-x86_64.tar.gz
	本地下载后scp到云服务，wget 下载比较慢
2. tar -axvf 解压
3. cp -r mysql-5.7.22-linux-glibc2.12-x86_64 /usr/local/mysql; 配置mysql bin路径到环境变量(不拷贝到/usr/local/下， bin/mysqld 初始化不成功)
4. 添加开机启动  cp mysql-5.7.22-linux-glibc2.12-x86_64/support-files/mysql.server  /etc/init.d/mysqld
	
	修改   vim /etc/init.d/mysqld   
	添加路径 在46行  
	basedir=/usr/local/mysql  
	datadir=/usr/local/mysql/data 
5. 添加系统mysql组     groupadd mysql

	添加mysql用户 useradd -r -g mysql mysql   （添加完成后可用id mysql查看）

6. 修改当前目录拥有者为mysql用户  chown -R mysql:mysql ./
7. 初始化数据库 (/user/local/mysql路径下)      bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data	
	#### <a name="fenced-code-block">初始化log中会显示暂时为root设置的密码</a>
8. 启动mysql

```
[root@iZuf64eonfsc2rxofbutcvZ bin]# /etc/init.d/mysqld start

Starting MySQL.The server quit without updating PID file (/[失败]n/mysqld/mysqld.pid).
```
上述问题是/etc/my.conf 配置文件导致
弃用/etc/my.conf 后成功启动mysql

10. 登录mysql mysql -uroot -p 上面初始化时的密码
11. 修改root密码(初次使用必须先设置root密码)
```
 	alter user 'root'@'localhost' identified by 'root';   
```
```
	flush privileges;    #刷新权限
```
12. 创建新用户(指定用户所拥有的db和权限)
```
GRANT ALL PRIVILEGES ON *.* TO 'root1'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;   #授权新用户
```

