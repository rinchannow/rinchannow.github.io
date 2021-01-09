---
layout: post
title: "Tomcat 闪退问题："A child container failed during start""
date: YYYY-MM-DD HH:MM:SS
categories: bugs
---

Tomcat 闪退，查看日志，报错如下：

```
09-Jan-2021 18:52:44.864 SEVERE [main] org.apache.catalina.core.ContainerBase.startInternal A child container failed during start
	java.util.concurrent.ExecutionException: org.apache.catalina.LifecycleException: A child container failed during start
```

往下看：

```
Caused by: org.apache.catalina.LifecycleException: Failed to start component [org.apache.catalina.webresources.StandardRoot@12c8a2c0]
```

根据网上信息，清除 Tomcat 缓存未果，排查 jar 包同样没有解决。于是考虑是否 Tomcat conf 目录下 server.xml 文件的原因，因为之前配置过 docBase，故将其删除，添加上这段代码：

```
 <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
```

重新启动，问题解决。