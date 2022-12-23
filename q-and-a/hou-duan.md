# 后端

## _hzero-report_

### 1、白屏

_hzero-report_ 服务需依赖

{% code overflow="wrap" lineNumbers="true" %}
```xml
<dependency>
    <groupId>org.hzero.starter</groupId>
    <artifactId>hzero-starter-report-xdo</artifactId>
</dependency>
```
{% endcode %}



## _hzero-platform_

### 1、批量 LOV 查询不支持主键加密

_hzero-platform_ 需升级版本

{% code overflow="wrap" lineNumbers="true" %}
```xml
<dependency>
    <groupId>org.hzero</groupId>
    <artifactId>hzero-platform-saas</artifactId>
    <version>1.9.3.BETA</version>
</dependency>

<!-- 依赖组件列表 -->
<dependency>
    <groupId>org.hzero.starter</groupId>
    <artifactId>hzero-starter-core</artifactId>
    <version>1.9.3.BETA.2</version>
</dependency>

<dependency>
    <groupId>org.hzero.boot</groupId>
    <artifactId>hzero-boot-platform</artifactId>
    <version>1.9.3.BETA</version>
</dependency>
```
{% endcode %}



## _hzero-import_

### 1、导入报主键加密错误

_hzero-starter-keyencrypt_ 需升级版本至 _`1.9.1.RELEASE`_

{% code overflow="wrap" lineNumbers="true" %}
```xml
<dependency>
    <groupId>org.hzero.starter</groupId>
    <artifactId>hzero-starter-keyencrypt</artifactId>
    <version>1.9.1.RELEASE</version>
</dependency>
```
{% endcode %}



## _hssp-service_

### 1、导入报主键加密错误

> 导入时基于 _`H1DetailsHelper`_ 获取变量解密报错

_hzero-starter-keyencrypt_ 需升级版本至 _`1.9.1.RELEASE`_

{% code overflow="wrap" lineNumbers="true" %}
```xml
<dependency>
    <groupId>org.hzero.starter</groupId>
    <artifactId>hzero-starter-keyencrypt</artifactId>
    <version>1.9.1.RELEASE</version>
</dependency>
```
{% endcode %}

{% hint style="info" %}
请一并升级 _hzero-import_ 的 _starter-keyencrypt_ 版本
{% endhint %}



## _hippius-submenu_

### 1、_hzero_ 合并库 _app_不能获取子应用

&#x20;需配置数据库前缀变量

{% code overflow="wrap" lineNumbers="true" %}
```json
database:
    prefix:
      hzeroPlatform: ${DATABASE_PRFIX_HZEROPLATFORM:HZERO}
```
{% endcode %}



## _hzero-boot-import_

### 1、_boot-import 与 boot-interface `poi` 不兼导入报错_

{% code overflow="wrap" lineNumbers="true" %}
```log
Exception in thread "hzero.import?" java.Lang. NoSuchMethodError Create breakpoint: 'org.apache.poi.xssf.model.SharedStringsTable org.apache.poi.xssf.eventusermodel.XSSFReac
at com.monitorbl.xlsx.impl.Streaminglorkbookreader.inittot
iva: 122)
at com.monitorjbi.xlsx.impl.StreamingWorkbookReader.init(StreaminqWorkbookReader.java:91)
at com.monitorjbi.xisx.StreamingReader$Builder.open(StreaminqReader.java:251)
at org.hzero.boot.imported.infra.execute. ExcelImportExecute.run (ExcelImportExecute. java:122) at org.hzero.boot.imported.infra.execute.strategy. DefaultImportExecuteStrategy. execute (DefaultImportExecutes
• java: 143)
```
{% endcode %}

&#x20;需将 _`boot-import`_ 的依赖顺序调至 _`boot-interface`_ 之前

{% code overflow="wrap" lineNumbers="true" %}
```xml
<dependency>
    <groupId>org.hzero.boot</groupId>
    <artifactId>hzero-boot-import</artifactId>
</dependency>

<dependency>
    <groupId>org.hzero.boot</groupId>
    <artifactId>hzero-boot-interface</artifactId>
</dependency>
```
{% endcode %}



## _hzero-boot-platform_

### 1、_boot-platform 更新 `1.9.3.RELEASE` 时缺少 HzeroServiceVisitorManager_&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```log
Caused by: java.lang.NoClassDefFoundError: org/hzero/common/HzeroServiceVisitorManager
	at java.lang.Class.getDeclaredMethods0(Native Method) ~[na:1.8.0_261]
	at java.lang.Class.privateGetDeclaredMethods(Class.java:2701) ~[na:1.8.0_261]
	at java.lang.Class.getDeclaredMethods(Class.java:1975) ~[na:1.8.0_261]
	at org.springframework.util.ReflectionUtils.getDeclaredMethods(ReflectionUtils.java:467) ~[spring-core-5.3.19.jar:5.3.19]
	... 35 common frames omitted
Caused by: java.lang.ClassNotFoundException: org.hzero.common.HzeroServiceVisitorManager
	at java.net.URLClassLoader.findClass(URLClassLoader.java:382) ~[na:1.8.0_261]
	at java.lang.ClassLoader.loadClass(ClassLoader.java:418) ~[na:1.8.0_261]
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:355) ~[na:1.8.0_261]
	at java.lang.ClassLoader.loadClass(ClassLoader.java:351) ~[na:1.8.0_261]
	... 39 common frames omitted
```
{% endcode %}

需将 _`hzero-starter-core`_ 一并升级至 _`1.9.3.RELEASE`_ 版本

{% code overflow="wrap" lineNumbers="true" %}
```xml
<dependency>
    <groupId>org.hzero.boot</groupId>
    <artifactId>hzero-boot-platform</artifactId>
    <version>1.9.3.RELEASE</version>
</dependency>

<dependency>
    <groupId>org.hzero.starter</groupId>
    <artifactId>hzero-starter-core</artifactId>
    <version>1.9.3.RELEASE</version>
</dependency>
```
{% endcode %}



## _hdsp-fr-server_

### 1、_帆软报表管理，上传报表文件时 `error.upload.multipartSize`异常_

{% code overflow="wrap" lineNumbers="true" %}
```log
Caused by: java.io.IOException: The temporary upload location [/tmp/tomcat.1658012614036908717.8574/work/Tomcat/localhost/ROOT] is not valid
        at org.apache.catalina.connector.Request.parseParts(Request.java:2877)
        at org.apache.catalina.connector.Request.parseParameters(Request.java:3242)
        at org.apache.catalina.connector.Request.getParameter(Request.java:1136)
        at org.apache.catalina.connector.RequestFacade.getParameter(RequestFacade.java:381)
        at org.springframework.web.filter.HiddenHttpMethodFilter.doFilterInternal(HiddenHttpMethodFilter.java:84)
```
{% endcode %}

`Spring Boot` 项目启动时会在`/tmp` 目录生成相关临时目录

{% code overflow="wrap" lineNumbers="true" %}
```bash
hsperfdata_root，
tomcat.************.8080
tomcat-docbase.*********.8080
```
{% endcode %}

`Multipart（form-data)`方式的请求时，默认会在第二个目录下创建临时文件，而 `CentOS` 会定时清理临时目录，导致目录不存在。可通过以下两种方式解决：

* 调整 `Spring Boot` 启动 `Tomcat` 目录

{% code lineNumbers="true" %}
```bash
-Dserver.tomcat.basedir=/home/tem
```
{% endcode %}

* 设置 `CentOS` 不删除临时目录

> `vim /usr/lib/tmpfiles.d/tmp.conf`
>
> 添加 `x /tmp/tomcat.*`

{% code overflow="wrap" lineNumbers="true" %}
```bash
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

# See tmpfiles.d(5) for details

# Clear tmp directories separately, to make them easier to override
v /tmp 1777 root root 10d    # 清理/tmp下10天前的目录和文件
v /var/tmp 1777 root root 30d    # 清理/var/tmp下30天前的目录和文件

# Exclude namespace mountpoints created with PrivateTmp=yes
x /tmp/systemd-private-%b-*
X /tmp/systemd-private-%b-*/tmp
x /tmp/tomcat.*
x /var/tmp/systemd-private-%b-*
X /var/tmp/systemd-private-%b-*/tmp
```
{% endcode %}
