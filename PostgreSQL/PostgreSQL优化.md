SQL是描述性语言,是一种介于关系演算(纯描述性的语言)和关系代数(一些基本的关系操作)之间的语言,
其中关系代数的基本操作包括：投影、选择、连接、并集、差集、重命名,并扩展出了外连接、半连接、聚集操作、分组操作等。
SQL语言可以转化为关系代数表达式,关系代数本身又有一些等价规则，因此可以对关系代数表达式进行等价转换。


1. 逻辑优化：基于规则的优化：基于关系代数等价规则做等价变换的优化（主要是建立在逻辑操作符上的优化）


内连接、外连接这些就是逻辑操作符。


2. 物理优化：基于代价的优化：就是建立在物理操作符上的优化，建立最优代价模型。


嵌套循环连接、哈希连接、归并连接这些就是物理操作符。


PostgreSQL 查询执行的基本流程：

![pg_optimizer](https://images.gitbook.cn/7740d080-cdf8-11e8-9819-c5f6b437e972)





SQL是描述性语言,是一种介于关系演算(纯描述性的语言)和关系代数(一些基本的关系操作)之间的语言,
其中关系代数的基本操作包括：投影、选择、连接、并集、差集、重命名,并扩展出了外连接、半连接、聚集操作、分组操作等。
SQL语言可以转化为关系代数表达式,关系代数本身又有一些等价规则，因此可以对关系代数表达式进行等价转换。


1. 逻辑优化：基于规则的优化：基于关系代数等价规则做等价变换的优化（主要是建立在逻辑操作符上的优化）


内连接、外连接这些就是逻辑操作符。


逻辑优化方法：子查询 & 子连接提升、表达式预处理、外连接消除、谓词下推、连接顺序交换、等价类推理
	<1>. 子查询 & 子连接提升、表达式预处理、外连接消除叫做【逻辑重写优化】，主要是对查询树进行改造。
	<2>. 谓词下推、连接顺序交换、等价类推理则可以称为【逻辑分解优化】

案例：
【谓词下推 + 等价类推理】：是为了尽早地过滤数据，这样就能在上层结点降低计算量。（常量谓词下推是推荐的）

SELECT sname FROM TEACHER t, COURSE c WHERE t.tno = 5 AND t.tno = c.tno;

修改为：

SELECT sname FROM (SELECT * FROM TEACHER WHERE tno = 5) tt, (SELECT cname, tno FROM COURSE) cc WHERE tt.tno = cc.tno;  -- 选择下推 + 投影下推


SELECT sname FROM (SELECT * FROM TEACHER WHERE tno = 5) tt, (SELECT cname, tno FROM COURSE WHERE tno=5) cc WHERE tt.tno = cc.tno; -- 等价推理


SELECT sname FROM (SELECT * FROM TEACHER WHERE tno = 5) tt, (SELECT cname, tno FROM COURSE WHERE tno=5) cc;  -- 


注意：内连接谓词下推，但外连接谓词可以下推吗？



2. 物理优化：基于代价的优化：就是建立在物理操作符上的优化，建立最优代价模型。

嵌套循环连接、哈希连接、归并连接这些就是物理操作符。


统计信息和选择率：PostgreSQL的物理优化需要计算各种物理路径的代价，而代价估算的过程严重依赖于数据库的统计信息。统计信息是否能准确地描述表中的数据分布情况是决定代价准确性的重要条件之一。
通过统计信息，代价估算系统就可以了解一个表有多少行数据、用了多少个数据页面、某个值出现的频率等，然后就能根据这些信息计算出一个约束条件能过滤掉多少数据，这种约束条件过滤出的数据占总数据量的比例称为选择率。

统计信息的形式：distinct率、NULL值率、高频值、直方图、相关系数

统计信息是基于采样的数据，因此也是不准确的。


物理路径：
	<1>. 扫描路径：顺序扫描路径（全表扫描）、索引扫描路径（回表随机读，因为存储的地址是有序的，但是数据就是无序的）、快速索引扫描路径（不用回表）、
位图扫描路径（通过位图将地址收集保存起来，让地址变得有序，通过中间的位图消解掉随机读）、TID 扫描路径（TID元组在磁盘上的存储地址）等
	<2>. 连接路径：嵌套循环连接路径、哈希连接路径、归并连接路径，另外还有一些其他的路径，比如排序路径、物化路径等
		 NL：时间复杂度：O(mn) 或者 O(mlogn)，如果内表走索引
		 HJ：时间复杂度：O(m * n /N)，其中N是内表哈希表的桶的个数，只能用于等值连接
		 SMJ：时间复杂度：

    这些是SPJ 路径，PostgreSQL 的优化器通常先生存 SPJ 路径,然后再叠加 Non-SPJ 路径（如：聚集操作、排序操作、limit 操作、分组操作……）


PostgreSQL采用顺序读写一个页面的IO代价作为单位1，而把随机IO定为了顺序IO的4倍


磁盘IO的代价单位：和page有关，主要包括，顺序IO和随机IO 
CPU代价基准单位：
总代价 = CPU 代价 + IO 代价 + 通信代价 



数据库路径的搜索方法：自底向上方法、自顶向下方法、随机方法 ，PostgreSQL主要采用了自底向上（动态规划）和随机方法（遗传算法）。开源优化器 ORCA 就使用了自顶向下的方法。

动态规划有两个特点：一个是要重复地利用子问题的解，这样能减少计算量，降低复杂度；另外一点就是通过子问题的最优解能够构造出最终的最优解，也就是说需要具有最优子结构的性质，所以动态规划的复杂度和穷举是不一样的。







PostgreSQL 查询执行的基本流程：

一个查询SQL语句在不同的阶段，生成的树是不同的，这些树的顺序应该是先生成语法树（词法分析和语法分析），然后得到查询树（关系代数表达式），
查询树就是查询优化器的输入，经过逻辑优化和物理优化，最终产生一颗最优的计划树，计划树就是我们说的执行计划。


SQL语句历程：
```
1. 语法分析：Lex工具对SQL进行词法分析并产生token(token都带固定词性，如：关键字，标识符，常量，运算符或者边界符等)，如：
SELECT   ---> 关键字
*        ---> 常量
FROM     ---> 关键字
TEST_A   ---> 常量
;        ---> 边界符

语法分析器（Yacc工具）接受token，并结合预定义好的语法规则生成语法树。


2. 语义分析：检查和转换 ---> 得到查询树
   检查对象是否存在，如果存在，就转换成内部形式保存，并从数据库元数据（如：pg_class、pg_attributes）中读取需要的信息。
SELECT   ----> 查询操作
*        ----> 投影, "*" 被展开成具体的列,不只是记录列名,而是通过该列在表中的“第几列”来表示
FROM TEST_A; ---> 要查询的表,通过表名找到该表的OID并且将表的所有信息组织成一个描述符。


3. 查询重写
pg_rewrite记录重写规则，如：视图重写，然后优化器进行逻辑优化提升、物理优化。


4. 打印执行计划的参数：GUC 参数可查看查询树和执行计划树
debug_pretty_print：打开该参数在打印查询树和执行计划时会以结构化的方式来展示，便于对查询树进行分析；
debug_print_parse：打开该参数可以打印查询树；
debug_print_rewritten：打开该参数可以打印重写（视图）之后的查询树；
debug_print_plan：打开该参数可以打印执行计划。

如：postgres=# SET DEBUG_PRINT_PLAN = ON;

```
一、解读执行计划：
执行计划是一个非完全的二叉树，每个父结点至少有一个子结点（叶子结点除外），最多有两个子结点。PostgreSQL 数据库的查询执行器通过对这个二叉树迭代执行来获得查询结果，它的执行过程我们通常叫它火山模型。

EXPLAIN 语句获取执行计划。

嵌套循环连接NL的执行流程：
1.如果不存在外表元组，从外边获得一条元组；
2.如果外表元组是 NULL，连接操作结束；
3.从内表获得一条元组；
4.如果内表元组是 NULL，跳转到步骤 1；
5.外表和内表元组做连接，返回连接结果。

时间复杂度是一个 O(MN），通常适用于：没有什么可用的连接条件 & 内表有索引，可以通过索引扫描加速

cost：执行这一步骤的代价，包含：启动代价（返回第一条元组前所消耗的代价，通常做一些“预处理”操作，如：排序）
rows：执行这一步骤会产生的元组数量，这是一个估计值。
width：产生出的元组的平均字节数（PG_TYPE.typlen中类型的长度）

物化：enable_material，如果返回数据量小，内存可以存放，建议物化。

```
EXPLAIN 语法说明：

EXPLAIN [ ( _option_ [, ...] ) ] _statement_

_option_值为：
ANALYZE [ _boolean_ ]：真实计划。
VERBOSE [ _boolean_ ]
COSTS [ _boolean_ ]
BUFFERS [ _boolean_ ]：和ANALYZE同时使用，打印缓冲区的命中率。
TIMING [ _boolean_ ]：和ANALYZE同时使用。
FORMAT { TEXT | XML | JSON | YAML } 
```

二、调整执行计划：扫描路径 + 连接路径 
GUC参数：SET GUC_NAME = ON/OFF;
```
postgres=# select name,setting,short_desc from pg_settings where name like 'enable_%';   
              name              | setting |                       short_desc                       
--------------------------------+---------+--------------------------------------------------------
 enable_bitmapscan              | on      | Enables the planner's use of bitmap-scan plans.
 enable_gathermerge             | on      | Enables the planner's use of gather merge plans.
 enable_hashagg                 | on      | Enables the planner's use of hashed aggregation plans.
 enable_hashjoin                | on      | Enables the planner's use of hash join plans.
 enable_hints                   | on      | Enable optimizer hints in SQL statements.           -- EDB专属
 enable_indexonlyscan           | on      | Enables the planner's use of index-only-scan plans.
 enable_indexscan               | on      | Enables the planner's use of index-scan plans.
 enable_material                | on      | Enables the planner's use of materialization.
 enable_mergejoin               | on      | Enables the planner's use of merge join plans.
 enable_nestloop                | on      | Enables the planner's use of nested-loop join plans.
 enable_parallel_append         | on      | Enables the planner's use of parallel append plans.
 enable_parallel_hash           | on      | Enables the planner's use of parallel hash plans.
 enable_partition_pruning       | on      | Enable plan-time and run-time partition pruning.
 enable_partitionwise_aggregate | off     | Enables partitionwise aggregation and grouping.
 enable_partitionwise_join      | off     | Enables partitionwise join.
 enable_seqscan                 | on      | Enables the planner's use of sequential-scan plans.
 enable_sort                    | on      | Enables the planner's use of explicit sort steps.
 enable_tidscan                 | on      | Enables the planner's use of TID scan plans.
```
聚集与分组的执行计划调整：
+ 哈希聚集（Hash Cluster) HashAggregate, 参数 enable_hashagg
+ 顺序聚集（Sort Cluster) GroupAggregate, 无参数

并行执行计划：表级PARALLEL_WORKERS参数：CREATE TABLE TEST_A(a INT) WITH (PARALLEL_WORKERS=100);
+ min_parallel_table_scan_size：启用并行表扫描的最小页面数， 也就是说表扫描的页面数小于 min_parallel_table_scan_size， 不会启用并行扫描
+ min_parallel_index_scan_size：启用并行索引扫描的最小页面数， 也就是说索引扫描的页面数小于 min_parallel_index_scan_size， 不会启用并行扫描
+ max_parallel_workers_per_gather：每个 gather 下的最大并行度， 在同一个执行计划里， gather 路径是并行的最上层子路径， 它用来对并行的后台线程的执行结果进行合并， 一个执行计划里可能有多个 gather 路径

如果：heap_pages < min_parallel_table_scan_size 或者 index_pages < min_parallel_index_scan_size ，就不启用并行查询。

+ max_parallel_workers：用来控制在同一时间最多有多少并行的进程。

+ force_parallel_mode：强制增加一个 gather 结点
