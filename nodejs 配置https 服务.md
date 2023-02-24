[步骤参考](https://blog.csdn.net/weixin_38946164/article/details/107981042)
在windows 上我用的git 的bash 才能正常使用 openssl 命令, 创建并cd到定目录下,依次运行命令就可以获得三个文件: privatekey.pem, certrequest.csr, certificate.pem

- 1.
```bash
 openssl genrsa -out privatekey.pem 1024
```

- 2.
```bash
openssl req -new -key privatekey.pem -out certrequest.csr
```

- 3.
```bash
openssl x509 -req -in certrequest.csr -signkey privatekey.pem -out certificate.pem
```

- 4. 拷贝 privatekey.pem  和 certificate.pem 到项目跟目录下的key 文件夹中, 这两个一个是证书私钥, 一个是自签名证书

- 5. 个人比较喜欢新的东西, 也爱偷懒, 于是用koa2 和 koa2 的脚手架, 安装之前先设置一下

查看当前 npm registry: ``` npm config get registry```
设置淘宝镜像: ```npm config set registry https://registry.npm.taobao.org```
安装脚手架: ```npm install -g koa-generator```
使用脚手架命令: ``` koa2 yourdir``` 回车, 然后进入文件夹里安装

- 6. 修改项目目录下的bin 文件夹下的 www 文件如下:

```js
#!/usr/bin/env node

/**
 * Module dependencies.
 */

var app = require('../app');
var debug = require('debug')('demo:server');
var http = require('http');
var https = require('https')
var fs = require('fs');

const options = {
  key: fs.readFileSync('./key/privatekey.pem'),
  cert: fs.readFileSync('./key/certificate.pem')
};

/**
 * Get port from environment and store in Express.
 */

var port = normalizePort(process.env.PORT || '3000');
var SSL_PORT = 4444;

// app.set('port', port);

/**
 * Create HTTP server.
 */

var server = http.createServer(app.callback());


https.createServer(options, app.callback()).listen(SSL_PORT);


/**
 * Listen on provided port, on all network interfaces.
 */

server.listen(port);
server.on('error', onError);
server.on('listening', onListening);




/**
 * Normalize a port into a number, string, or false.
 */

function normalizePort(val) {
  var port = parseInt(val, 10);

  if (isNaN(port)) {
    // named pipe
    return val;
  }

  if (port >= 0) {
    // port number
    return port;
  }

  return false;
}

/**
 * Event listener for HTTP server "error" event.
 */

function onError(error) {
  if (error.syscall !== 'listen') {
    throw error;
  }

  var bind = typeof port === 'string'
    ? 'Pipe ' + port
    : 'Port ' + port;

  // handle specific listen errors with friendly messages
  switch (error.code) {
    case 'EACCES':
      console.error(bind + ' requires elevated privileges');
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(bind + ' is already in use');
      process.exit(1);
      break;
    default:
      throw error;
  }
}

/**
 * Event listener for HTTP server "listening" event.
 */

function onListening() {
  var addr = server.address();
  var bind = typeof addr === 'string'
    ? 'pipe ' + addr
    : 'port ' + addr.port;
  debug('Listening on ' + bind);
}

```

- 7. npm run dev 在项目文件夹下, 然后浏览器 https://localhost:4444 , 开始可能会拦截警告, 因为这个证书是个人做的,不是第三方. 直接继续访问就可以了.

![image](https://user-images.githubusercontent.com/10356819/221135602-d33942be-7417-4bab-bded-8ca5faba6bfc.png)



