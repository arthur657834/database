```
下载mariadb
https://downloads.mariadb.org/

备注：MariaDB_5.x.x和MariaDB_10.x.x区别
MariaDB_5.x.x：兼容MySQL5.x.x的，接口几乎一致，只限于社区版
MariaDB_10.x.x：10.x.x使用新技术，接口会与mysql逐渐区别开来。目标就是以后想MariaDB新接口过渡

mysql -uroot -pRoot_123! -h 10.1.50.186
SHOW GLOBAL VARIABLES LIKE 'plugin_dir';

cp server_audit.so /usr/lib64/mysql/plugin/

INSTALL PLUGIN server_audit SONAME 'server_audit.so';
UNINSTALL PLUGIN server_audit;
select * from information_schema.plugins;

show plugins;
set global server_audit_events='QUERY';
set global server_audit_logging='ON';

show global variables like '%server_audit%';

vi /etc/my.cnf
[mysqld]
server_audit_events='CONNECT,QUERY,TABLE,QUERY_DDL,QUERY_DML,QUERY_DCL'
备注：指定哪些操作被记录到日志文件中
server_audit_logging=on
server_audit_file_path=/var/lib/mysql/
备注：审计日志存放路径，该路径下会生成一个server_audit.log文件，就会记录相关操作记录了,mysql用户一定要有读写权限
server_audit_file_rotate_size=200000000
#server_audit_file_rotate_size=2G
server_audit_file_rotations=200
server_audit_file_rotate_now=ON



systemctl restart mysqld

防止server_audit 插件被卸载，需要在配置文件中添加:
[mysqld]
server_audit=FORCE_PLUS_PERMANENT
重启MySQL生效

配置解析：
https://mariadb.com/kb/en/mariadb/server_audit-system-variables/
https://mariadb.com/kb/en/library/mariadb-audit-plugin-log-settings/
```
