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
  + 11
  + 11
+ [Character set support](https://dev.mysql.com/doc/refman/8.0/en/charset-unicode-sets.html)：默认字符集从 latin1 变为 utf8mb4，包含新的collations，如：utf8mb4_ja_0900_as_cs。
+ **JSON enhancements**
  + 11
  + 11
+ [Data type support](https://dev.mysql.com/doc/refman/8.0/en/data-type-defaults.html)： BLOB, TEXT, GEOMETRY, 和 JSON 数据类型,支持expressions作为默认值。
+ **Optimizer**
  + 11
  + 11
+ [Common table expressions](https://dev.mysql.com/doc/refman/8.0/en/with.html)：CTE 支持 nonrecursive 和 recursive 两种类修改。
+ [Window functions](https://dev.mysql.com/doc/refman/8.0/en/window-functions.html)
+ [Lateral derived tables](https://dev.mysql.com/doc/refman/8.0/en/lateral-derived-tables.html)
+ **Aliases in single-table DELETE statements**：MySQL 8.0.16+版本开始支持
+ [Regular expression support](https://dev.mysql.com/doc/refman/8.0/en/regexp.html)：支持 REGEXP_LIKE()/REGEXP/RLIKE、REGEXP_INSTR()、 REGEXP_REPLACE()、 REGEXP_SUBSTR()函数， 系统变量 regexp_stack_limit 和 regexp_time_limit 控制资源消耗。
+ Internal temporary tables：TempTable替换MEMORY，作为默认内部内存临时表存储引擎。受系统变量internal_tmp_mem_storage_engine 和 temptable_max_ram 控制。
+ [Logging](https://dev.mysql.com/doc/refman/8.0/en/error-log.html)：受系统变量 log_error_services  控制。
+ Backup lock：允许在线备份过程中执行DML操作。需要 BACKUP_ADMIN 权限，支持 LOCK INSTANCE FOR BACKUP 和 UNLOCK INSTANCE 语法。
+ Replication
+ Connection management
+ Configuration
  + 11
  + 11
+ Plugins
+ C API


---
#### 二、Features Deprecated




---
#### 三、Features Removed
