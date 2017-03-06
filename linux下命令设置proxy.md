### 记录下linux下一些命令设置proxy

不用挨个去查询help，在这里记录下，常用的看的次数多了就记住了。

#### 1. linux bash

  export http_proxy=http://ip+port

#### 2. apt-get

  这个主要是ubuntu用，找到apt.conf文件，在里面这么配置：

  ```javascript

    Acquire::http::proxy "http://username:password@host:port_no/";
    Acquire::https::proxy "https://username:password@host:port_no/";
    Acquire::ftp::proxy "ftp://username:password@host:port_no/";
    Acquire::socks::proxy "socks://username:password@host:port_no/";

  ```

#### 3. apt-key

  apt-key adv **--keyserver-options http-proxy=<myProxy>** --keyserver keyserver.ubuntu.com --recv 7F0CEB10

#### 4. docker

  这个直接看官网的文档吧：[docker http_proxy](https://docs.docker.com/engine/admin/systemd/#http-proxy)