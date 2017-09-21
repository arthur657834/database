```
1 禁用validate-password

编辑my.cnf配置文件，在mysqld下面加入“validate-password=OFF”,然后重启mysql即可。

2 降低安全策略级别

首相我们来看一下validate-password相关的参数：

validate-password=ON/OFF/FORCE/FORCE_PLUS_PERMANENT: 决定是否使用该插件(及强制/永久强制使用)。

validate_password_dictionary_file：插件用于验证密码强度的字典文件路径。

validate_password_length：密码最小长度。

validate_password_mixed_case_count：密码至少要包含的小写字母个数和大写字母个数。

validate_password_number_count：密码至少要包含的数字个数。

validate_password_policy：密码强度检查等级，0/LOW、1/MEDIUM、2/STRONG。

validate_password_special_char_count：密码至少要包含的特殊字符数。

其中，关于validate_password_policy-密码强度检查等级：

0/LOW：只检查长度。

1/MEDIUM：检查长度、数字、大小写、特殊字符。

2/STRONG：检查长度、数字、大小写、特殊字符字典文件。

我们可以将安全策略降低为LOW，相信这样虽然还会有长度限制，但是已经足够简单了。


INSTALL PLUGIN validate_password SONAME 'validate_password.so';


测试：
grant  all on *.* to tester@'localhost' identified by 'tasssss';
```
