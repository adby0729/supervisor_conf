Supervisor install
===============
	sudo pip install supervisor
	  https://github.com/adby0729/supervisor_conf/blob/master/init.d/supervisor 放置到 /etc/init.d/ 下 
	  我们可以看到启动脚本中，其实默认写了一个启动参数 -c /etc/supervisord.conf 

Supervisor Config 
===============
	1. 生成配置文件
	  $ echo_supervisord_conf > /etc/supervisord.conf
	2.修改配置文件
	  vi /etc/supervisord.conf
	找到
	  [include]
	  files = /etc/supervisor/conf.d/*.conf
	
	  然后再/etc/supervisor/conf.d/ 目录里放.conf文件。
	  比如example.conf

	  [program:example-8888]
	  command=/var/www/example/server.py --port=8888
	  autostart=true ; supervisord守护程序启动时自动启动tornado
	  autorestart=true ; supervisord守护程序重启时自动重启tornado
	  redirect_stderr=true ; 将stderr重定向到stdout
	  user=www-data<br>
	  directory=/var/www/example ; cd 到应用目录
	  stdout_logfile = /var/www/example/log/server-8888.log
	  [program:example]<br>
	  command=/home/php/bin/php src/main.php
	  user=root
	  directory=/home/application/jobman/
	  autostart=true
	  startsecs=10
	  autorestart=true
	  startretries=8640
