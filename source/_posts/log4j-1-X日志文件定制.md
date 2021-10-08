---
title: log4j-1.X日志文件定制
date: 2020-02-14 14:11:33
tags: [日志, log4j]
---
最近写的定时小任务太多了，都是独立工程不好管理。如果合并工程，每个任务独立记录日志，好管理一点，日志也不会混乱。

log4j默认的配置文件是log4j.properties（详见org.apache.log4j.LogManager.java）
配置项顶层是：
log4j.rootLogger

语法为：log4j.rootLogger = 【日志级别】,loggerName,loggerName1,...
例如
log4j.rootLogger=DEBUG,Console,File

这里Console和File是我们自定义的，DEBUG（必须大写）是日志级别

自定义日志：
因为要分割日志，所以我们要再定义一个
log4j.logger.myQuartz = DEBUG,myQuartz

配合log4j.additivity.myQuartz = false
就可以把日志信息从总文件里分离出来

接着设置appender
log4j.appender.myQuartz = org.apache.log4j.RollingFileAppender
log4j.appender.myQuartz.File = logs/myQuartz.log
log4j.appender.myQuartz.MaxFileSize = 10MB
log4j.appender.myQuartz.MaxBackupIndex = 10
log4j.appender.myQuartz.Threshold = ALL
log4j.appender.myQuartz.layout = org.apache.log4j.PatternLayout
log4j.appender.myQuartz.ConversionPattern = [%p] [%d{yyyy-MM-dd HH\:mm\:ss}][%c]%m%n
log4j.appender.myQuartz.encoding = UTF-8
log4j.appender.myQuartz.append = true

使用时,指定Logger名称就可以了
LoggerFactory.getLogger("myQuartz")

但是如果再来一个log4j.logger.myQuartz2怎么办?
不得不把所有配置再写一遍：
log4j.logger.myQuartz2 = DEBUG,myQuartz2
...

properties地狱？?   ->>to be continued