```
[mysqld]
default_authentication_plugin=sha256_password


sha256_password_private_key_path=/usr/local/mysql/myprivkey.pem
sha256_password_public_key_path=/usr/local/mysql/mypubkey.pem

命令行连接mysql时需指定 --ssl-mode=required

GRANT INSERT,DELETE,UPDATE,SELECT ON test.user TO 'foo'@'localhost';
flush privileges;

grant select,update on *.* to ljtest3@localhost identified by 'DBuser123!';
flush privileges;

show variables like '%password%';

select @@old_passwords;

set old_passwords=2;


select password('B123456a!'),length(password('B123456a!'));

SELECT @@session.old_passwords, @@global.old_passwords;

```
