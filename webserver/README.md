Apache Webserver Test
========

* Base Image : ubuntu:18.04



```dockerfile
# Docker file
FROM ubuntu:18.04
LABEL maintainer="Cheolwon Lee <chlwn.lee@gmail.com>"

# install webserver
RUN apt-get update \
    && apt-get install -y apache2
RUN echo "TEST WEB" > /var/www/html/index.html
EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]
```



```shell
# build & run
$ docker build -t webserver:v1 .
$ docker run -d -p 80:80 --name web webserver
```

```shell
# Test
$ curl localhost:80
TEST WEB
```
