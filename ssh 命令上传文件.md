
### ssh user@xxx.xxx.xxx.xxx 用户登陆远程服务器, 回车后输入密码即可

### windows 如果要scp copy文件到远程linux服务器 则不能先登陆, 而是一条命令 scp c:/xxx.txt user@xxx.xxx.xxx.xxx:/home/user/www  回车输入密码

[关于文件拷贝](https://www.cnblogs.com/zdz8207/p/linux-cp-dir.html)

拷贝文件下的东西, 而不是整个文件夹:  ``` cp -r dir1/.  dir2``` 前提是dir2存在, 如果不存在就用 ```cp -r dir1 dir2```
