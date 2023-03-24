
[参考](https://www.cnblogs.com/taiyonghai/p/9402734.html), windows 版本

cd 到目录下:
开启服务器: start nginx
查看服务器进程是否起来: tasklist /fi "imagename eq nginx.exe"
关闭服务器: nginx -s stop
查看配置文件是否配置正确: nginx -t -c conf/nginx.conf


实测有效

```
  server {
        listen       8080;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        # location / {
        #     root   html;
        #     index  index.html index.htm;
        # }
		
	location / {
	     proxy_pass http://localhost:3000/;
	}
 }
```
