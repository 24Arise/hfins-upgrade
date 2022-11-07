# 后端

## _hzero-report_

### 1、白屏

_hzero-report_ 服务需依赖

{% code lineNumbers="true" %}
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

{% code lineNumbers="true" %}
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
