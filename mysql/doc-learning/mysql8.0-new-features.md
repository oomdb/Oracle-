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
  + grant授权表存储引擎由 MyISAM 变为 InnoDB 。
  + [caching_sha2_password 认证插件](https://dev.mysql.com/doc/refman/8.0/en/caching-sha2-pluggable-authentication.html)：SHA-256算法实现，与sha256_password插件一样。比mysql_native_password插件更安全。caching_sha2_password是默认的认证插件。
  + [支持角色Roles](https://dev.mysql.com/doc/refman/8.0/en/roles.html) 
  + 


---
#### 二、Features Deprecated




---
#### 三、Features Removed
