### MySQL 通用安装指南
--- 
**1. 平台支持**

支持主流的操作系统平台，32位或者64位等,如：
+ Unix, Linux, FreeBSD
+ Microsoft Windows
+ OS X 

  详见：[MySQL主流版本支持平台](https://www.mysql.com/support/supportedplatforms/database.html)

**2. 选择分发版本**
  
  常用MySQL分发版本：
  + 二进制（推荐）
  + 源码
  
  MySQL分发版本的演进路线：
  + 开发版
  + GA版 
  
  比如：mysql-8.0.1-dmr
  + **第1个数字**：主版本号
  + **第2个数字**：次版本号，主版本号+次版本号 = 发布序列号（描述稳定的功能集）
  + **第3个数字**：发行版系列中的版本号，新bug修复，值都会累加，建议选择最新版本
  
  后缀表明发行版的稳定性级别（DMR -> RC -> GA）：
  + **dmr**：表示开发里程碑版本（DMR）
  + **rc**：稳定，通过所有内部测试，继续引入新特性，重点修复bugs
  + **缺失后缀**：GA 或 生产版本，GA版本是稳定的，已成功通过早期版本阶段，并且被认为是可靠的，没有严重的错误，并且适用于生产系统

**3. 下载分发版本**

  下载地址：
  + [官方地址](https://dev.mysql.com/downloads/)
  + [官方镜像地址](https://dev.mysql.com/downloads/mirrors/)

  各平台Repo安装方式
  + **MySQL Yum Repository**：RPM-based Linux platforms.
  + **MySQL APT Repository**：Debian-based Linux platforms.
  + **MySQL SLES Repository**：SUSE Linux Enterprise Server (SLES) platforms.

**4. 验证包完整性**

**5. 安装分发版**

**6. 安装后设置**

**7. MySQL benchmark（Perl）**
