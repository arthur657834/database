```
--skip-networking

Do not listen for TCP/IP connections at all. All interaction with mysqld must be made using named pipes or shared memory (on Windows) or Unix socket files (on Unix). This option is highly recommended for systems where only local clients are permitted. See Section 8.12.5.2, “DNS Lookup Optimization and the Host Cache”.

bind-address : 你需要绑定的IP地址.

skip-networking ： 开启 skip-networking 选项可以彻底关闭MySQL的TCP/IP连接方式，在一些文档中也提到在单机运行的 MySQL 推荐开启该选项，不太靠谱。

开启该选项之后：
  windows：
    开启shared_memory=ON或enable-named-pipe 选项，连接的时候指定--protocol=memory或--protocol=pipe
    mysql --protocol=pipe -u root -p
    mysql -uroot -pw123123 --protocol=memory
  unix：
    使用socket连接 -S /tmp/mysql.sock

当mysql登陆时，同时指定-h和-S，mysql会默认使用tcp/ip的方式连接。

mysql登陆的时候，指定参数-h，会使用tcp/ip的方式连接，如果没有指定端口的话，默认是使用3306端口

当什么参数都没有指定的时候，mysql默认使用socket方式登陆，如果my.cnf的[client]没有指定socket文件路径时，mysql默认会去寻找/tmp/mysql.sock，所以如果mysql服务启动的时候，生成的socket文件不是默认路径的话，登陆会报错。

小结：安装了多实例的情况下，需要登录到特定端口实例下的方法
  1. 使用“-S” 参数，通过指定实例下的socket文件来登录到指定的实例
  2. 使用“-h”参数，注意，这里必须是使用'TCP/IP'的方式，不能是'localhost'，因为'localhost'会使用默认的socket文件登录

https://dev.mysql.com/doc/refman/5.7/en/server-options.html
    
tips:
  1. MySQL本地连接，如果不指mysql --protocol=tcp, 连接默认是socket方式连接的。这点大家都知道。 
  2. MySQL socket连接是根据sokect文件来的，与--port不相关的，如果是一机多实例，则用-S(或者--socket=name ）来指定连接哪个实例。

perror 111
//查看错误原因
    
```
