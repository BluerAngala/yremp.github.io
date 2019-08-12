---
title: Spring Boot 日志配置
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: ./
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-7-23 18:16:01
comments: true
tags: 
 - web
 - Spring Boot
keywords: Spring Boot 
description: Spring Boot日志文件可以在服务遇到问题时可以根据日志文件快速定位问题所在，解决问题。1.Spring Boot 日志级别：Debug->INFO->WARN->ERROR 2. Spring Boot 默认日志级别：INFO
photos: https://yremp.live/wp-content/uploads/2019/07/69447264_p3.png
---
<!-- wp:heading {"level":3} -->
<h3>1.日志文件</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Spring Boot 日志级别：Debug-&gt;INFO-&gt;WARN-&gt;ERROR</li><li> Spring Boot  默认日志级别：INFO</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>2.控制台输出级别控制</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>（1）application.properties 中配置：ROOT代表默认全局设置</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>logging.level.ROOT=INFO        //默认输出INFO以上包括INFO级别的日志</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>（2）application.properties中配置： 单独控制包的日志输出级别 </h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>logging.level.org.apache=ERROR  //只有EEEOR信息才会输出到控制台</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>3.将日志写到指定文件</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>（1）在 application.properties 设置日志文件目录：</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>logging.file=F:/logs/document.log</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>（2）使用logback.xml自定义日志文件输出 </h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>logback.xml和application.properties在同一个目录下</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```
 &lt;?xml version="1.0" encoding="UTF-8"?>
 &lt;configuration  scan="true" scanPeriod="60 seconds" debug="false">
    &lt;contextName>projectName&lt;/contextName>
    &lt;property name="contextName" value="projectName" />
    &lt;property name="log_dir" value="./logs/" />
    &lt;!--输出到控制台-->
    &lt;appender name="console" class="ch.qos.logback.core.ConsoleAppender">
        &lt;!-- 级别过滤器。如果日志级别低于WARN，将被过滤掉。 ALL TRACE DEBUG INFO WARN ERROR-->
        &lt;filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            &lt;level>DEBUG&lt;/level>
        &lt;/filter>
        &lt;encoder>
            &lt;pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} %-5level %msg - %file:%line%n&lt;/pattern>
            &lt;charset>UTF-8&lt;/charset>
        &lt;/encoder>
    &lt;/appender>
    
    &lt;!-- 每天记录info级别日志文件 -->
    &lt;appender name="InfoRollingFileAppender"
        class="ch.qos.logback.core.rolling.RollingFileAppender">
        &lt;Prudent>true&lt;/Prudent>
        &lt;layout class="ch.qos.logback.classic.PatternLayout">
            &lt;Pattern>%d{yyyy-MM-dd HH:mm:ss} %-5level %msg - %file:%line%n&lt;/Pattern>
        &lt;/layout>
        &lt;rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            &lt;FileNamePattern>${log_dir}/${contextName}_info%d{yyyy-MM-dd}.log
            &lt;/FileNamePattern>
        &lt;/rollingPolicy>
        &lt;!-- 级别过滤器。如果日志级别低于WARN，将被过滤掉。ALL TRACE DEBUG INFO WARN ERROR-->
        &lt;filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            &lt;level>INFO&lt;/level>
        &lt;/filter>
        &lt;!-- 除了DEBUG级别的日志，其它什么级别的日志都不要 -->
        &lt;!-- &lt;filter class="ch.qos.logback.classic.filter.LevelFilter">
            &lt;level>DEBUG&lt;/level>
            &lt;level>INFO&lt;/level>
            &lt;onMatch>ACCEPT&lt;/onMatch>
            &lt;onMismatch>DENY &lt;/onMismatch>
        &lt;/filter> -->
    &lt;/appender>
    
    &lt;!-- 每天记录ERROR级别日志文件 -->
    &lt;appender name="ErrorRollingFileAppender"
        class="ch.qos.logback.core.rolling.RollingFileAppender">
        &lt;Prudent>true&lt;/Prudent>
        &lt;layout class="ch.qos.logback.classic.PatternLayout">
            &lt;Pattern>%d{yyyy-MM-dd HH:mm:ss} %-5level %msg - %file:%line%n&lt;/Pattern>
        &lt;/layout>
        &lt;rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            &lt;FileNamePattern>${log_dir}/${contextName}_error%d{yyyy-MM-dd}.log
            &lt;/FileNamePattern>
        &lt;/rollingPolicy>
        &lt;!-- 级别过滤器。如果日志级别低于WARN，将被过滤掉。 -->
        &lt;filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            &lt;level>ERROR&lt;/level>
        &lt;/filter>
        &lt;!-- 除了DEBUG级别的日志，其它什么级别的日志都不要 -->
        &lt;!-- &lt;filter class="ch.qos.logback.classic.filter.LevelFilter">
            &lt;level>DEBUG&lt;/level>
            &lt;level>INFO&lt;/level>
            &lt;onMatch>ACCEPT&lt;/onMatch>
            &lt;onMismatch>DENY &lt;/onMismatch>
        &lt;/filter> -->
    &lt;/appender>

    &lt;root>
        &lt;appender-ref ref="console" />
        &lt;appender-ref ref="InfoRollingFileAppender" />
        &lt;appender-ref ref="ErrorRollingFileAppender" />
    &lt;/root>
 &lt;/configuration>
```
<!-- /wp:code -->

<!-- wp:paragraph {"textColor":"vivid-red"} -->
<p class="has-text-color has-vivid-red-color">使用logback.xml，上面  properties 中日志配置将全部失效</p>
<!-- /wp:paragraph -->