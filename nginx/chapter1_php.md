
#nginx 配置代理 php

 1. 安装php 和 php-fpm（FastCGI Process Manager：FastCGI）php的解释器
 2. 启动php-fpm（FastCGI Process Manager：FastCGI进程管理器)是一个PHPFastCGI管理器。解释器(cgi)
 ```
php-fpm --fpm-config /usr/local/var/php-fpm.conf  --prefix /usr/local/var
```
 3. 安装nginx
 4. 第一种打开nginx默认的php配置： 
```
 fastcgi_param  SCRIPT_FILENAME  /Users/land/work/php$fastcgi_script_name;
 ```
 指定php项目所在路径
 5. 配置多个php项目：
	
	<b>
	实验环境

	阿里云ECS + centos + Nginx + php-fpm
	
	项目1
	
	1.工程路径： /data/wwwroot/project1/
	
	2.访问路径： http://www.dev.com/project1/
	
	项目2
	
	1.工程路径： /data/wwwroot/project2/
	
	2.访问路径： http://www.dev.com/project2/
	</b>
	
	```
	location ^~ /project1 { 
		 alias /data/wwwroot/project1; 
		 try_files $uri $uri/ @project1;
		 location ~ .php$ { 
			fastcgi_pass unix:/dev/shm/php-cgi.sock; 
			fastcgi_index index.php;
			 fastcgi_param  SCRIPT_FILENAME  /data/wwwroot$fastcgi_script_name;
		}
	}
	location @project1{ 
		rewrite /project1/(.*)$ /project1/index.php?/$1 last;
	}
	
	```
	
##### 结果(car是php的一个项目文件夹)
 
 ```
	 location ^~ /car {
	 
	        index  index.html index.htm index.php;
	        alias /Users/land/work/php/car;
	        try_files $uri $uri/ @car;
	        location ~ .php$ {
	            index  index.html index.htm index.php;
	            root           /Users/land/work/php;
	                fastcgi_pass   127.0.0.1:9000;
	                fastcgi_index index.php;
	        #       fastcgi_param _FILENAME $request_filename;
	                fastcgi_param  SCRIPT_FILENAME  /Users/land/work/php$fastcgi_script_name;
	                include fastcgi_params;
	        }
	}
	location @car{
	        rewrite /car/(.*)$ /car/index.php?/$1 last;
	}
	
```
	
#注意点：出现file not found 

php-fpm 所有者非root用户
