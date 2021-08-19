## CentOS操作系统下的源码编译安装

### 一、安装

1. 创建一个存放源码的目录

   ```BASH
   [root@ff4da083e253 ~]# mkdir ~/soft
   ```

2. 切换到上述创建的目录下，在Redis[官网](http://redis.cn)下载源码

   ```bash
   [root@ff4da083e253 ~]# cd soft/
   [root@ff4da083e253 soft]# wget http://download.redis.io/releases/redis-6.0.6.tar.gz
   ```

3. 解压下载的源码包

   ```bash
   [root@ff4da083e253 soft]# tar -zxvf redis-6.0.6.tar.gz
   ```

4. 安装gcc并进入解压目录，编译源码(因为源码是C语言写的，需要gcc编译)

   ```bash
   [root@ff4da083e253 soft]# yum install -y gcc
   [root@ff4da083e253 soft]# cd redis-6.0.6
   [root@ff4da083e253 redis-6.0.6]# make
   ```

5. 编译完成后，安装在指定目录下(如果不知道目录，则会安装在默认目录`/usr/local/bin`)

   ```bash
   [root@ff4da083e253 redis-6.0.6]# make install PREFIX=/opt/wuliang/redis6
   ```

### 二、启动

1. 添加Redis环境变量

   ```bash
   [root@ff4da083e253 redis-6.0.6]# vi /etc/profile
   # 打开文件后，在末尾追加如下内容：
   export REDIS_HOME=/opt/wuliang/redis6
   export PATH=$PATH:$REDIS_HOME/bin
   ```

2. 根据源码提供的脚本，启动Redis

   ```bash
   [root@ff4da083e253 redis-6.0.6]# ./utils/install_server.sh
   ...
   Please select the redis port for this instance: [6379]
   Selecting default: 6379
   Please select the redis config file name [/etc/redis/6379.conf]
   Selected default - /etc/redis/6379.conf
   Please select the redis log file name [/var/log/redis_6379.log]
   Selected default - /var/log/redis_6379.log
   Please select the data directory for this instance [/var/lib/redis/6379]
   Selected default - /var/lib/redis/6379
   Please select the redis executable path [/opt/wuliang/redis6/bin/redis-server]
   Selected config:
   Port           : 6379
   Config file    : /etc/redis/6379.conf
   Log file       : /var/log/redis_6379.log
   Data dir       : /var/lib/redis/6379
   Executable     : /opt/wuliang/redis6/bin/redis-server
   Cli Executable : /opt/wuliang/redis6/bin/redis-cli
   Is this ok? Then press ENTER to go on or Ctrl-C to abort.
   Copied /tmp/6379.conf => /etc/init.d/redis_6379
   Installing service...
   Successfully added to chkconfig!
   Successfully added to runlevels 345!
   Starting Redis server...
   Installation successful!
   ```

   > 从上述可以看到，会以端口号区分不同的Redis实例以及对应配置文件、日志文件、数据持久化目录等资源。

3. 查看服务状态

   > 上述脚本执行完成后，同时会自动创建一个service服务(/etc/init.d目录下，就可以看到，此处为：redis_6379)

   ```bash
   [root@ff4da083e253 redis-6.0.6]# service redis_6379 status
   Redis is running (13917)
   ```

