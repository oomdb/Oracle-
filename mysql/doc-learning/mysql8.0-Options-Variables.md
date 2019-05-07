### MySQL8.0 Server and Status Variables and Options
--- 
+ Options and Variables Introduced in MySQL 8.0
+ Options and Variables Deprecated in MySQL 8.0
+ Options and Variables Removed in MySQL 8.0

---
#### 一、Options and Variables Introduced
+ 111

---
#### 二、Options and Variables Deprecated
+ **expire_logs_days**：清理二进制日志时间周期，MySQL 8.0.3
+ **innodb_undo_tablespaces**：回滚段表空间文件数量，MySQL 8.0.4
+ **log_syslog**：是否将错误日志写入syslog，MySQL 8.0.2
+ **no-dd-upgrade**：阻止启动时自动升级数据字典表，MySQL 8.0.16
+ **symbolic-links**：允许MyISAM表建立符号链接，MySQL 8.0.2 

---
#### 三、Options and Variables Removed
+ **Com_alter_db_upgrade**：统计ALTER DATABASE ... UPGRADE DATA DIRECTORY NAME语句数量，MySQL 8.0.0
+ **Innodb_available_undo_logs**：显示InnoDB回滚段的总数量，不同于innodb_rollback_segments变量（显示活跃的回滚段数量），MySQL 8.0.2
+ **Qcache_free_blocks**：查询缓存（QC）中的可用内存块数，MySQL 8.0.3
+ **Qcache_free_memory**：查询缓存（QC）的可用内存量，MySQL 8.0.3
+ **Qcache_hits**：查询缓存（QC）命中数，MySQL 8.0.3
+ **Qcache_inserts**：查询缓存（QC）插入的数量，MySQL 8.0.3
+ **Qcache_lowmem_prunes**：由于缓存中缺少可用内存而从查询缓存（QC）中删除的查询数，MySQL 8.0.3
+ **Qcache_not_cached**：非缓存查询（QC）的数量（由于query_cache_type设置而无法缓存或未缓存），MySQL 8.0.3
+ **Qcache_queries_in_cache**：在查询缓存（QC）中注册的查询数，MySQL 8.0.3
+ **Qcache_total_blocks**：查询缓存（QC）中的块总数，MySQL 8.0.3
