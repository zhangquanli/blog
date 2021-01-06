# flowable问题汇总

## 1. 启动项目中，flowable直接报错，提示`Table 'flowable.ACT_GE_PROPERTY' doesn't exist`

```java
java.sql.SQLSyntaxErrorException: Table 'flowable.ACT_GE_PROPERTY' doesn't exist
```

### 原因分析

- 一方面的原因：当前的MySQL数据库已经部署过Flowable并自动创建过表，开发过程中手动删除了Flowable自动创建的表。Flowable查找MySQL的元数据时，搜索到了删除过的历史表。因此，Flowable在判断表是否存在时，出现了一定的问题。

- 二方面的原因：`MySQL 8.0` 版本驱动将参数`nullCatalogMeansCurrent` 的默认值由true改为了false，如果使用DatabaseMetaData.getTables获取所有的表信息，包含了历史表记录，导致误判。 

### 解决方法

- 把正常的数据库的表导出为sql，手动创建表。 

-  mysql的连接字符串中添加上`nullCatalogMeansCurrent=true`，设置为只查当前连接的schema库。 

  ```yaml
  spring:
    datasource:
      driver-class-name: com.mysql.jdbc.Driver
      url: jdbc:mysql://127.0.0.1:3306/flowable?useUnicode=true&characterEncoding=UTF-8&serverTimezone=Asia/Shanghai&nullCatalogMeansCurrent=true
      username: root
      password: root
  ```

  