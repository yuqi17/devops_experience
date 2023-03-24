
[参考](https://www.cnblogs.com/taiyonghai/p/9402734.html)

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
