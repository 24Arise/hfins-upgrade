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

