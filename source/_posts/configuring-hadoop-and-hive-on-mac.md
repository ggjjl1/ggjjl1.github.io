---
title: 在 Mac 上配置 Hadoop-2.6.2 和 Hive-1.2.1 遇到问题
date: 2015-11-25 12:08:27
tags: [Mac OSX,hadoop,hive]
---
问题描述：
在 Mac 上安装配置完 Hadoop-2.6.2 后，再安装 Hive-1.2.1 并启动，出现以下错误信息。
```
    gjl: ~/bin/apache-hive-1.2.1-bin $bin/hive
    
    Logging initialized using configuration in jar:file:/Users/gaojunliang/bin/apache-hive-1.2.1-bin/lib/hive-common-1.2.1.jar!/hive-log4j.properties
    [ERROR] Terminal initialization failed; falling back to unsupported
    java.lang.IncompatibleClassChangeError: Found class jline.Terminal, but interface was expected
        at jline.TerminalFactory.create(TerminalFactory.java:101)
        at jline.TerminalFactory.get(TerminalFactory.java:158)
        at jline.console.ConsoleReader.<init>(ConsoleReader.java:229)
        at jline.console.ConsoleReader.<init>(ConsoleReader.java:221)
        at jline.console.ConsoleReader.<init>(ConsoleReader.java:209)
        at org.apache.hadoop.hive.cli.CliDriver.setupConsoleReader(CliDriver.java:787)
        at org.apache.hadoop.hive.cli.CliDriver.executeDriver(CliDriver.java:721)
        at org.apache.hadoop.hive.cli.CliDriver.run(CliDriver.java:681)
        at org.apache.hadoop.hive.cli.CliDriver.main(CliDriver.java:621)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at org.apache.hadoop.util.RunJar.run(RunJar.java:221)
        at org.apache.hadoop.util.RunJar.main(RunJar.java:136)
    
    Exception in thread "main" java.lang.IncompatibleClassChangeError: Found class jline.Terminal, but interface was expected
        at jline.console.ConsoleReader.<init>(ConsoleReader.java:230)
        at jline.console.ConsoleReader.<init>(ConsoleReader.java:221)
        at jline.console.ConsoleReader.<init>(ConsoleReader.java:209)
        at org.apache.hadoop.hive.cli.CliDriver.setupConsoleReader(CliDriver.java:787)
        at org.apache.hadoop.hive.cli.CliDriver.executeDriver(CliDriver.java:721)
        at org.apache.hadoop.hive.cli.CliDriver.run(CliDriver.java:681)
        at org.apache.hadoop.hive.cli.CliDriver.main(CliDriver.java:621)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at org.apache.hadoop.util.RunJar.run(RunJar.java:221)
        at org.apache.hadoop.util.RunJar.main(RunJar.java:136)
```

解决办法：
将 Hive 中的 jline 从 2.x 版本降级到 1.x 之后，将 Hadoop 中 share/hadoop/yarn/lib 目录下的 jline 升级到 2.x 版本。

