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
+ **Slave_heartbeat_period**：Slave库复制心跳间隔，单位：秒，MySQL 8.0.1
+ **Slave_last_heartbeat**：以TIMESTAMP格式显示收到最新心跳信号的时间，MySQL 8.0.1
+ **Slave_received_heartbeats**：自上次重置以来从Slave接收的心跳数，MySQL 8.0.1 
+ **Slave_retried_transactions**：自启动以来Slave端SQL线程已重试事务的总次数，MySQL 8.0.1 
+ **Slave_running**：Slave库 I/O thread 状态，MySQL 8.0.1 
+ **bootstrap**：mysql安装脚本使用，MySQL 8.0.0
+ **date_format:**：DATE格式 (未使用)，MySQL 8.0.3
+ **datetime_format**：DATETIME/TIMESTAMP格式(未使用)，MySQL 8.0.3
+ **des-key-file:**：从给定文件加载des_encrypt() 和 des_encrypt 密钥，MySQL 8.0.3
+ **group_replication_allow_local_disjoint_gtids_join**：允许当前服务器加入该组，即使该组中没有事务，MySQL 8.0.4  
+ **have_crypt**：crypt() 系统调用的可用性，MySQL 8.0.3
+ **ignore-builtin-innodb**：忽略内置InnoDB，MySQL 8.0.3
+ **ignore-db-dir**：将目录视为非数据库目录，MySQL 8.0.0
+ **ignore_db_dirs**：目录被视为非数据库目录，MySQL 8.0.0 
+ **innodb_checksums**：启用InnoDB checksums校验，MySQL 8.0.0 
+ **innodb_disable_resize_buffer_pool_debug**：禁用InnoDB缓冲池的大小调整，MySQL 8.0.0 
+ **innodb_file_format**： 新InnoDB表的格式，MySQL 8.0.0
+ **innodb_file_format_check**：InnoDB是否执行文件格式兼容性检查，MySQL 8.0.0 
+ **innodb_file_format_max**：共享表空间中的文件格式标记，MySQL 8.0.0
+ **innodb_large_prefix**：为列前缀索引启用更长的键，MySQL 8.0.0 
+ **innodb_locks_unsafe_for_binlog**：强制InnoDB不使用next-key锁定，而仅使用行级锁定，MySQL 8.0.0 
+ **innodb_scan_directories**：定义InnoDB恢复期间扫描表空间文件目录，MySQL 8.0.4 
+ **innodb_stats_sample_pages**：索引分布统计信息采样的索引页数，MySQL 8.0.0 
+ **innodb_support_xa**：启用InnoDB支持XA事务的二阶段提交，MySQL 8.0.0
+ **innodb_undo_logs**：定义InnoDB使用的undo logs (rollback segments)数量，是innodb_rollback_segments 变量的别名，MySQL 8.0.2 
+ **internal_tmp_disk_storage_engine**：内部临时表存储引擎，MySQL 8.0.16 
+ **log-warnings**：记录非关键warnings信息到日志文件，MySQL 8.0.3 
+ **log_builtin_as_identified_by_password**：是否以向后兼容的方式记录CREATE / ALTER USER，GRANT 语句，MySQL 8.0.11 
+ **log_error_filter_rules**：错误日志过滤规则，MySQL 8.0.4 
+ **log_syslog**：是否记录错误日志到syslog中，MySQL 8.0.13 
+ **log_syslog_facility**：syslog 信息工具，MySQL 8.0.13 
+ **log_syslog_include_pid**：是否在syslog信息中报告 server PID，MySQL 8.0.13 
+ **log_syslog_tag**：在syslog信息中记录服务器标识符，MySQL 8.0.13 
+ **max_tmp_tables**：未使用，MySQL 8.0.3
+ **metadata_locks_cache_size**：metadata锁缓冲大小，MySQL 8.0.13 
+ **metadata_locks_hash_instances**：metadata锁hash数量 ，MySQL 8.0.13
+ **multi_range_count**：在范围选择期间一次发送到表处理程序的最大范围数，MySQL 8.0.3 
+ **old_passwords**：为PASSWORD()函数选择密码哈希方法，MySQL 8.0.11 
+ **partition**：分区支持的启用或者禁用，MySQL 8.0.0
+ **query_cache_limit**：缓存结果集的最大限制，MySQL 8.0.3
+ **query_cache_min_res_unit**：分配结果空间的最小单位大小（在写完所有结果数据后将修剪最后一个单位），MySQL 8.0.3 
+ **query_cache_size**：分配用于存储旧查询结果的内存，MySQL 8.0.3 
+ **query_cache_type**：查询缓存（QC）类型，MySQL 8.0.3
+ **query_cache_wlock_invalidate**：在LOCK上查询缓存中的无效查询进行写入，MySQL 8.0.3  
+ **secure-auth**：不允许使用pre-4.1 之前的密码进行账户认证，MySQL 8.0.3 
+ **show_compatibility_56**：兼容 SHOW STATUS/VARIABLES 语句，MySQL 8.0.1
+ **skip-partition**：不启用用户自定义分区，MySQL 8.0.0
+ **sync_frm**：创建时同步.frm文件到磁盘，默认启用，MySQL 8.0.0
+ **temp-pool**：使用此选项将导致创建的大多数临时文件使用一小组名称，而不是每个新文件的唯一名称。，MySQL 8.0.1
+ **time_format**：TIME格式（未使用） ，MySQL 8.0.3 
+ **tx_isolation**： 默认事务隔离级别，MySQL 8.0.3
+ **tx_read_only**：默认事务访问模式，MySQL 8.0.3 

