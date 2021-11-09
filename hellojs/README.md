Hello JS
========

* Base Image : node:12
* file : hello.js

> node:12 이미지를 기반으로 hello.js 를 실행한다.
> hello.js 는 8080 포트를 Listen 하며 컨테이너 아이디를 출력한다.

```dockerfile
# Docker file
FROM node:12
COPY hello.js /
CMD ["node", "/hello.js"]
```

```javascript
// hello.js
const http = require('http');
const os = require('os');
console.log('Test server starting...');

var handler = function (request, response) {
    console.log('Received request from ' + request.connection.remoteAddress);
    response.writeHead(200);
    response.end('Container Hostname: ' + os.hostname() + '\n');
};

var www = http.createServer(handler);
www.listen(8080);
```


```shell
# build & run
$ docker build -t hellojs:latest .
$ docker run -d -p 8080:8080 --name web hellojs
```

```shell
# Test
$ curl localhost:8080
Container Hostname: 120090b700e5
```
