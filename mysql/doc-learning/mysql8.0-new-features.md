### MySQL8.0 New Features
--- 
+ Features Added in MySQL 8.0
+ Features Deprecated in MySQL 8.0
+ Features Removed in MySQL 8.0

---
#### 一、Features Added
+ [MySQL Data dictionary](https://dev.mysql.com/doc/refman/8.0/en/data-dictionary.html)
+ [Atomic data definition statements (Atomic DDL)](https://dev.mysql.com/doc/refman/8.0/en/atomic-ddl.html)
+ [Upgrade procedure](https://dev.mysql.com/doc/refman/8.0/en/upgrading-what-is-upgraded.html)：MySQL 8.0.16版本开始，安装新版本数据库，在下次启动时，自动调用mysql_upgrade执行升级任务。
+ **Security and account management**
  + mysql库下的 grant授权表 存储引擎由 MyISAM 变为 InnoDB 。
  + [caching_sha2_password 认证插件](https://dev.mysql.com/doc/refman/8.0/en/caching-sha2-pluggable-authentication.html)：SHA-256算法实现，与sha256_password插件一样。比mysql_native_password插件更安全。caching_sha2_password是默认的认证插件。
  + [支持角色Roles](https://dev.mysql.com/doc/refman/8.0/en/roles.html) 
  + [包含用户账户类别](https://dev.mysql.com/doc/refman/8.0/en/account-categories.html)：通过 SYSTEM_USER 权限区分 系统用户 和 普通用户。
  + [授予全局权限](https://dev.mysql.com/doc/refman/8.0/en/partial-revokes.html):受需要变量 partial_revokes 控制。
  + GRANT ...  AS user [WITH ROLE]。
  + [密码管理策略](https://dev.mysql.com/doc/refman/8.0/en/password-management.html)
  + [支持FIPS模式](https://dev.mysql.com/doc/refman/8.0/en/fips-mode.html)
  + [运行时重配新连接的 SSL context](https://dev.mysql.com/doc/refman/8.0/en/using-encrypted-connections.html#using-encrypted-connections-server-side-runtime-configuration)
  + [OpenSSL 1.1.1支持TLS v1.3加密协议](https://dev.mysql.com/doc/refman/8.0/en/encrypted-connection-protocols-ciphers.html)
  + MySQL现在将授予命名管道上的客户端的访问控制设置为Windows上成功通信所必需的最小值：受 named_pipe_full_access_group 系统变量控制。
+ [Resource management](https://dev.mysql.com/doc/refman/8.0/en/resource-groups.html)
+ [Table encryption management](https://dev.mysql.com/doc/refman/8.0/en/innodb-tablespace-encryption.html#innodb-schema-tablespace-encryption-default)：受 default_table_encryption 和 table_encryption_privilege_check 系统变量控制，有 TABLE_ENCRYPTION_ADMIN 权限。
+ **InnoDB enhancements**
  +
  +
+ Character set support
+ **JSON enhancements**
  +
  + 
+ Data type support
+ **Optimizer**
  + 
  + 
+ Common table expressions
+ Window functions
+ Lateral derived tables
+ Aliases in single-table DELETE statements
+ Regular expression support
+ Internal temporary tables
+ Logging
+ Backup lock
+ Replication
+ Connection management
+ Configuration
  +
  + 
+ Plugins
+ C API


---
#### 二、Features Deprecated




---
#### 三、Features Removed
