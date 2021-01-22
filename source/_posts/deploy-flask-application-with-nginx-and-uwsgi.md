---
title: Nginx+uwsgi部署flask应用
date: 2015-10-27 20:19:00
tags: [Linux,Python,Flask]
---
一、准备工作
1.ubuntu 14.04
2.python 2.7
3.nginx 1.4.6(apt-get install安装)
4.uwsgi(apt-get install安装)
5.flask(pip install安装)

二、配置
1.nginx配置
cd到nginx安装目录，ubuntu下使用apt-get安装默认路径是 /etc/nginx
nginx的配置文件为nginx.conf
看到最后面两行
	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
发现 nginx配置了启动时夹在conf.d下面的配置文件
2.在conf.d下新建一个配置文件为 zhou.conf（命名随意）
加入如下内容：
```
    # zhou.conf
    # configuration of the server
    server {
        listen      80;
    
        location / {
            include uwsgi_params;
            uwsgi_pass 127.0.0.1:8001;
        }
    }
```
保存，退出。
重新载入nginx配置文件 nginx -s reload

3.启动uwsgi
cd到应用根目录，比如 /root/www
执行命令：
uwsgi --socket 127.0.0.1:8001 --wsgi-file hello.py --callable app --processes 4 --threads 2 --stats 127.0.0.1:9191

解释：--wsgi-file hello.py  其中hello.py为应用入口文件 
若要让uwsgi以守护进程运行，可添加参数 --daemonize /var/log/uwsgi.log


参考：
［1］[http://heipark.iteye.com/blog/1847421](http://heipark.iteye.com/blog/1847421)
［2］[http://docs.jinkan.org/docs/flask/deploying/uwsgi.html](http://docs.jinkan.org/docs/flask/deploying/uwsgi.html)
