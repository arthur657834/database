```
安装完成之后会生成临时密码，可以去日志里面看

mysql -uroot -p
pe1jM__qRY&u

Root_123!

show variables like '%ssl%'; 
SHOW VARIABLES LIKE 'have_ssl';
SHOW STATUS LIKE 'Ssl_cipher';
\s <==> status;



安装过程中生成对秘钥在/var/lib/mysql
[mysqld]
ssl-ca=ca.pem
ssl-cert=server-cert.pem
ssl-key=server-key.pem

服务端
自己生成
openssl genrsa 2048 > ca-key.pem
openssl req -sha1 -new -x509 -nodes -days 3650 -key ca-key.pem > ca-cert.pem
openssl req -sha1 -newkey rsa:2048 -days 730 -nodes -keyout server-key.pem > server-req.pem

将服务器的私钥导出成RSA类型的密钥。
openssl rsa -in server-key.pem -out server-key.pem

使用CA证书，创建服务器证书
openssl x509 -sha1 -req -in server-req.pem -days 730 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 > server-cert.pem

客户端：
openssl req -sha1 -newkey rsa:2048 -days 730 -nodes -keyout client-key.pem > client-req.pem
openssl rsa -in client-key.pem -out client-key.pem
openssl x509 -sha1 -req -in client-req.pem -days 730 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 > client-cert.pem

GRANT ALL PRIVILEGES ON *.* TO 'ljtest'@'%' IDENTIFIED BY 'Ljtest123!' REQUIRE SSL;
FLUSH PRIVILEGES;

client:
mysql --ssl-ca=ca-cert.pem --ssl-cert=client-cert.pem --ssl-key=client-key.pem -u ljtest -p
或者
[client]
ssl-ca=/path/to/ca-cert.pem
ssl-cert=/path/to/client-cert.pem
ssl-key=/path/to/client-key.pem

JDBC连接

在jdbc字符串中增加下面参数
useSSL=true&verifyServerCertificate=false
这么就不需要客户端配置证书了，配置就简单很多。因为mysql本身有账号口令认证，因此不需要证书认证。

```
