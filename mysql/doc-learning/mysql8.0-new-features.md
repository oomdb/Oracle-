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
  + [授予全局权限](https://dev.mysql.com/doc/refman/8.0/en/partial-revokes.html):受系统变量 partial_revokes 控制。
  + GRANT ...  AS user [WITH ROLE]。
  + [密码管理策略](https://dev.mysql.com/doc/refman/8.0/en/password-management.html)
  + [支持FIPS模式](https://dev.mysql.com/doc/refman/8.0/en/fips-mode.html)
  + [运行时重配新连接的 SSL context](https://dev.mysql.com/doc/refman/8.0/en/using-encrypted-connections.html#using-encrypted-connections-server-side-runtime-configuration)
  + [OpenSSL 1.1.1支持TLS v1.3加密协议](https://dev.mysql.com/doc/refman/8.0/en/encrypted-connection-protocols-ciphers.html)
  + MySQL现在将授予命名管道上的客户端的访问控制设置为Windows上成功通信所必需的最小值：受 named_pipe_full_access_group 系统变量控制。
+ [Resource management](https://dev.mysql.com/doc/refman/8.0/en/resource-groups.html)
+ [Table encryption management](https://dev.mysql.com/doc/refman/8.0/en/innodb-tablespace-encryption.html#innodb-schema-tablespace-encryption-default)：受 default_table_encryption 和 table_encryption_privilege_check 系统变量控制，有 TABLE_ENCRYPTION_ADMIN 权限。
+ **InnoDB enhancements**
  + 最大 auto-increment 值持久化(MySQL服务重启)
  + 记录索引树冲突记录到redo log，保证 crash safe
  + [memcached 插件支持多get操作和range 查询](https://dev.mysql.com/doc/refman/8.0/en/innodb-memcached-multiple-get-range-query.html)
  + 支持死锁检测参数 innodb_deadlock_detect 动态调整
  + 新增INFORMATION_SCHEMA.INNODB_CACHED_INDEXES表，报告每个索引在InnoDB缓冲池中缓存的索引页数innodb_rollback_segments 系统参数定义每个undo表空间回滚段的数量，之前是整个MySQL实例
  + InnoDB 临时表创建在ibtmp1共享临时表空间中
  + InnoDB 表空间加密特性，支持：redo log 和 undo log 数据加密
  + [SELECT ... FOR SHARE 和 SELECT ... FOR UPDATE 语句支持 NOWAIT 和 SKIP LOCKED 选项](https://dev.mysql.com/doc/refman/8.0/en/innodb-locking-reads.html#innodb-locking-reads-nowait-skip-locked)
  + 支持 ALTER TABLE [ADD|DROP|COALESCE|REORGANIZE|REBUILD] PARTITION，使用 ALGORITHM={COPY|INPLACE} 和 LOCK 语句。
  + [InnoDB使用MySQL data dictionary存储引擎相关的数据字典信息](https://dev.mysql.com/doc/refman/8.0/en/data-dictionary.html)
  + mysql系统表和数据字典表开始存储在mysql.ibd独立表空间中，之前是存放在mysql数据库目录个人InnoDB表空间文件中
  + 独立undo表空间，MySQL 8.0.14+开始，支持undo表空间的CREATE/DROP/ALTER 在线操作
  + innodb_undo_log_truncate 系统参数默认开启
  + innodb_rollback_segments 系统参数定义每个undo表空间回滚段的数量，之前是整个MySQL实例回滚段的数量
  + innodb_max_dirty_pages_pct_lwm 默认值从 0 变为 10，innodb_max_dirty_pages_pct 默认值从 75 变为 90
  + [innodb_autoinc_lock_mode 系统参数默认值为 2](https://dev.mysql.com/doc/refman/8.0/en/innodb-auto-increment-handling.html#innodb-auto-increment-lock-modes)
  + 支持重命名通用表空间，ALTER TABLESPACE ... RENAME TO 
  + [新增innodb_dedicated_server系统参数，默认关闭，自动配置 innodb_buffer_pool_size/innodb_log_file_size/innodb_flush_method 3个参数值](https://dev.mysql.com/doc/refman/8.0/en/innodb-dedicated-server.html)
  + 新增 INFORMATION_SCHEMA.INNODB_TABLESPACES_BRIEF 表空间视图
  + 内置压缩库 zlib library 版本从 1.2.3 变为 1.2.11
  + 序列化字典信息（SDI）存在于除temp表空间和undo表空间文件之外的所有InnoDB表空间文件中
  + [支持 原子DDL](https://dev.mysql.com/doc/refman/8.0/en/atomic-ddl.html)
  + [MySQL服务停止时，可以通过innodb_directories选项move表空间文件到新位置](https://dev.mysql.com/doc/refman/8.0/en/innodb-moving-data-files-offline.html)
  + [redo log 优化](https://dev.mysql.com/doc/refman/8.0/en/optimizing-innodb-logging.html)：新增 innodb_log_wait_for_flush_spin_hwm/innodb_log_spin_cpu_abs_lwm/innodb_log_spin_cpu_pct_hwm 3个参数 以及 innodb_log_buffer_size 系统参数可在线动态调整
  + MySQL 8.0.12+版本，undo支持对lob对象的细微更新（100 bytes 以内 ）
  + [在线DDL操作](https://dev.mysql.com/doc/refman/8.0/en/innodb-online-ddl-operations.html)MySQL 8.0.12+版本，ALTER TABLE 操作支持 ALGORITHM=INSTANT，如：添加列/添加、删除虚拟列/添加、删除列默认值/修改ENUM 或者 SET 列的定义/修改索引类型/重命名表。
  + MySQL 8.0.13+版本，TempTable存储引擎支持存储BLOB类型列。之前存储在 internal_tmp_disk_storage_engine 系统变量中。
  + MySQL 8.0.13+版本，InnoDB 静态数据（data-at-rest）加密特性支持general表空间。之前只支持独立表空间。
  + 禁用 innodb_buffer_pool_in_core_file 系统变量，使用此变量，core_file 变量必须开启 & OS必须支持 madvise()。
  + MySQL 8.0.13+版本，用户临时表和内部临时表存储在session会话临时表空间，之前存错在global临时表空间（ibtmp1）。innodb_temp_tablespaces_dir 和 INNODB_SESSION_TEMP_TABLESPACES 表，ibtmp1存储用户创建临时表空间的回滚段信息。
  + MySQL 8.0.14+版本，InnoDB 支持并发聚焦索引扫描，不支持二级索引。innodb_parallel_read_threads 参数设置大于1。默认是 4。
  + MySQL 8.0.14+版本，启用 innodb_dedicated_server  系统参数。
  + MySQL 8.0.14+版本，CREATE TABLESPACE语句的 ADD DATAFILE 字句是可选的，且不需要FILE权限。
  + [MySQL 8.0.16+版本，temptable_use_mmap 和 temptable_max_ram 系统变量](https://dev.mysql.com/doc/refman/8.0/en/internal-temporary-tables.html#internal-temporary-tables-engines)
  + [MySQL 8.0.16+版本，InnoDB 静态数据（data-at-rest）加密特性支持mysql系统表空间](https://dev.mysql.com/doc/refman/8.0/en/innodb-tablespace-encryption.html)
  + [MySQL 8.0.16+版本，新增 innodb_spin_wait_pause_multiplier 系统参数](https://dev.mysql.com/doc/refman/8.0/en/innodb-performance-spin_lock_polling.html)
+ [Character set support](https://dev.mysql.com/doc/refman/8.0/en/charset-unicode-sets.html)：默认字符集从 latin1 变为 utf8mb4，包含新的collations，如：utf8mb4_ja_0900_as_cs。
+ **JSON enhancements**
  + 1
  + 
  + 
  +
  +
  +
  +
  +
  +
  +
+ [Data type support](https://dev.mysql.com/doc/refman/8.0/en/data-type-defaults.html)： BLOB, TEXT, GEOMETRY, 和 JSON 数据类型,支持expressions作为默认值。
+ **Optimizer**
  + [支持不可见索引（invisible indexes）](https://dev.mysql.com/doc/refman/8.0/en/invisible-indexes.html)
  + [支持降序索引（descending indexes）](https://dev.mysql.com/doc/refman/8.0/en/descending-indexes.html)
  + [支持表达式索引（Functional key parts）](https://dev.mysql.com/doc/refman/8.0/en/create-index.html)
  + [MySQL 8.0.14+ 版本，在准备阶段删除where条件中的常量表达式，而不是等到优化阶段](https://dev.mysql.com/doc/refman/8.0/en/outer-join-optimization.html)
  + [MySQL 8.0.16+ 版本，支持 Constant-Folding Optimization ](https://dev.mysql.com/doc/refman/8.0/en/constant-folding-optimization.html)
  + [MySQL 8.0.16+ 版本，半连接优化，IN 子查询可以转换为 EXISTS 子查询](https://dev.mysql.com/doc/refman/8.0/en/semi-joins.html)
+ [Common table expressions](https://dev.mysql.com/doc/refman/8.0/en/with.html)：CTE 支持 nonrecursive 和 recursive 两种类修改。
+ [Window functions](https://dev.mysql.com/doc/refman/8.0/en/window-functions.html)
+ [Lateral derived tables](https://dev.mysql.com/doc/refman/8.0/en/lateral-derived-tables.html)
+ **Aliases in single-table DELETE statements**：MySQL 8.0.16+版本开始支持
+ [Regular expression support](https://dev.mysql.com/doc/refman/8.0/en/regexp.html)：支持 REGEXP_LIKE()/REGEXP/RLIKE、REGEXP_INSTR()、 REGEXP_REPLACE()、 REGEXP_SUBSTR()函数， 系统变量 regexp_stack_limit 和 regexp_time_limit 控制资源消耗。
+ Internal temporary tables：TempTable替换MEMORY，作为默认内部内存临时表存储引擎。受系统变量internal_tmp_mem_storage_engine 和 temptable_max_ram 控制。
+ [Logging](https://dev.mysql.com/doc/refman/8.0/en/error-log.html)：受系统变量 log_error_services  控制。
+ **Backup lock**：允许在线备份过程中执行DML操作。需要 BACKUP_ADMIN 权限，支持 LOCK INSTANCE FOR BACKUP 和 UNLOCK INSTANCE 语法。
+ [Replication](https://dev.mysql.com/doc/refman/8.0/en/json.html#json-partial-updates)：使用compact二进制格式，支持JSON documents 的部分更新，受系统参数binlog_row_value_options = PARTIAL_JSON 控制。
+ [Connection management](https://dev.mysql.com/doc/refman/8.0/en/client-connections.html)：允许专门为管理连接 配置TCP/IP端口。
+ **Configuration**：整个MySQL中主机名的最大允许长度已从以前的60个字符提高到255个ASCII字符。主要分布在 mysql system schema, Performance Schema, INFORMATION_SCHEMA, 和 sys schema;CHANGE MASTER TO 的 MASTER_HOST值；SHOW PROCESSLIST 输出的 host 列；账户名中的host名称；主机相关的命令选型和系统变量。
+ **Plugins**：之前是C 或者 C++，目前只能是 C++。
+ [C API](https://dev.mysql.com/doc/refman/8.0/en/c-api-asynchronous-interface.html)：MySQL CAPI 现在支持异步函数，用于与MySQL服务器进行非阻塞通信。

---
#### 二、Features Deprecated




---
#### 三、Features Removed
