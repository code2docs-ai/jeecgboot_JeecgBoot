# 基础信息

|      |      |
|------|------|
| 名称 | SysDataSourceServiceImpl |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/system/service/impl/SysDataSourceServiceImpl.java |
| 包名 | org.jeecg.modules.system.service.impl |
| 依赖项 | ['com.baomidou.dynamic.datasource.DynamicRoutingDataSource', 'com.baomidou.dynamic.datasource.creator.DataSourceProperty', 'com.baomidou.dynamic.datasource.creator.druid.DruidDataSourceCreator', 'com.baomidou.mybatisplus.core.conditions.query.QueryWrapper', 'com.baomidou.mybatisplus.extension.service.impl.ServiceImpl', 'org.apache.commons.lang.StringUtils', 'org.jeecg.common.api.vo.Result', 'org.jeecg.common.util.dynamic.db.DataSourceCachePool', 'org.jeecg.modules.system.entity.SysDataSource', 'org.jeecg.modules.system.mapper.SysDataSourceMapper', 'org.jeecg.modules.system.service.ISysDataSourceService', 'org.jeecg.modules.system.util.SecurityUtil', 'org.springframework.beans.factory.annotation.Autowired', 'org.springframework.stereotype.Service', 'javax.sql.DataSource'] |
| 概述说明 | 实现数据源增删改查，支持动态添加删除，确保编码唯一性。 |

# 说明

该内容描述了一个功能模块，主要实现数据源的增删改查操作。具体包括动态添加和删除数据源的功能，以及在添加或修改数据源时检查编码的唯一性，确保数据源编码不重复。这些功能旨在提供灵活的数据源管理，同时保证数据的完整性和唯一性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| SysDataSourceServiceImpl | class | 实现数据源增删改查，动态添加删除数据源，检查编码唯一性。 |



## 类 SysDataSourceServiceImpl

|      |      |
|------|------|
| 访问范围 | @Service;public |
| 类型 | class |
| 名称 | SysDataSourceServiceImpl |
| 说明 | 实现数据源增删改查，动态添加删除数据源，检查编码唯一性。 |


### UML类图

```mermaid
classDiagram
    class SysDataSourceServiceImpl {
        -DruidDataSourceCreator dataSourceCreator
        -DataSource dataSource
        +Result saveDataSource(SysDataSource sysDataSource)
        +Result editDataSource(SysDataSource sysDataSource)
        +Result deleteDataSource(String id)
        -void addDynamicDataSource(SysDataSource sysDataSource, String dbPassword)
        -void removeDynamicDataSource(String code)
        -long checkDbCode(String dbCode)
    }

    class DruidDataSourceCreator {
        +DataSource createDataSource(DataSourceProperty dataSourceProperty)
    }

    class DataSource {
        <<Interface>>
    }

    class DynamicRoutingDataSource {
        +void addDataSource(String code, DataSource dataSource)
        +void removeDataSource(String code)
    }

    class DataSourceProperty {
        -String url
        -String password
        -String driverClassName
        -String username
        +void setUrl(String url)
        +void setPassword(String password)
        +void setDriverClassName(String driverClassName)
        +void setUsername(String username)
    }

    class Result {
        +static Result error(String message)
        +static Result OK(String message)
    }

    class SysDataSource {
        -String id
        -String code
        -String dbPassword
        -String dbUrl
        -String dbDriver
        -String dbUsername
        +String getCode()
        +String getDbPassword()
        +void setDbPassword(String dbPassword)
        +String getDbUrl()
        +String getDbDriver()
        +String getDbUsername()
        +String getId()
    }

    class DataSourceCachePool {
        +static void removeCache(String code)
    }

    class SecurityUtil {
        +static String jiami(String password)
    }

    class StringUtils {
        +static boolean isNotBlank(String str)
    }

    class QueryWrapper~T~ {
        +LambdaQueryWrapper~T~ lambda()
    }

    class LambdaQueryWrapper~T~ {
        +LambdaQueryWrapper~T~ eq(boolean condition, SFunction~T, R~ column, Object val)
    }

    SysDataSourceServiceImpl --> DruidDataSourceCreator : 依赖
    SysDataSourceServiceImpl --> DataSource : 依赖
    SysDataSourceServiceImpl --> DynamicRoutingDataSource : 依赖
    SysDataSourceServiceImpl --> DataSourceProperty : 依赖
    SysDataSourceServiceImpl --> Result : 依赖
    SysDataSourceServiceImpl --> SysDataSource : 依赖
    SysDataSourceServiceImpl --> DataSourceCachePool : 依赖
    SysDataSourceServiceImpl --> SecurityUtil : 依赖
    SysDataSourceServiceImpl --> StringUtils : 依赖
    SysDataSourceServiceImpl --> QueryWrapper~SysDataSource~ : 依赖
    DynamicRoutingDataSource --> DataSource : 依赖
    DruidDataSourceCreator --> DataSourceProperty : 依赖
    QueryWrapper~SysDataSource~ --> LambdaQueryWrapper~SysDataSource~ : 依赖
```

这段代码定义了一个`SysDataSourceServiceImpl`类，该类负责管理数据源的增删改查操作。它依赖于多个外部类和工具类，如`DruidDataSourceCreator`、`DataSource`、`DynamicRoutingDataSource`等，用于创建、删除和动态管理数据源。`SysDataSourceServiceImpl`类通过调用这些依赖类的方法，实现了对数据源的加密、校验和缓存管理等功能。


### 内部方法调用关系图

```mermaid
graph TD
    A["类SysDataSourceServiceImpl"]
    B["属性: DruidDataSourceCreator dataSourceCreator"]
    C["属性: DataSource dataSource"]
    D["方法: Result saveDataSource(SysDataSource sysDataSource)"]
    E["方法: Result editDataSource(SysDataSource sysDataSource)"]
    F["方法: Result deleteDataSource(String id)"]
    G["私有方法: void addDynamicDataSource(SysDataSource sysDataSource, String dbPassword)"]
    H["私有方法: void removeDynamicDataSource(String code)"]
    I["私有方法: long checkDbCode(String dbCode)"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I

    D --> I["调用checkDbCode"]
    D --> G["调用addDynamicDataSource"]
    E --> H["调用removeDynamicDataSource"]
    E --> G["调用addDynamicDataSource"]
    F --> H["调用removeDynamicDataSource"]
```

```mermaid
sequenceDiagram
    participant A as SysDataSourceServiceImpl
    participant B as checkDbCode
    participant C as addDynamicDataSource
    participant D as removeDynamicDataSource
    participant E as save
    participant F as updateById
    participant G as removeById

    A->>B: 调用checkDbCode
    B-->>A: 返回count
    A->>E: 调用save
    E-->>A: 返回result
    A->>C: 调用addDynamicDataSource
    C-->>A: 返回
    A->>F: 调用updateById
    F-->>A: 返回result
    A->>D: 调用removeDynamicDataSource
    D-->>A: 返回
    A->>G: 调用removeById
    G-->>A: 返回
```

这段代码是一个Spring服务类`SysDataSourceServiceImpl`，主要负责数据源的增删改操作。代码中包含了多个方法，如`saveDataSource`、`editDataSource`和`deleteDataSource`，分别用于保存、编辑和删除数据源。此外，还有一些私有方法如`addDynamicDataSource`和`removeDynamicDataSource`，用于动态添加和删除数据源。代码通过调用这些方法，实现了对数据源的管理，并且在操作过程中进行了数据源编码的检查、密码加密等处理。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| dataSourceCreator | DruidDataSourceCreator | 自动注入Druid数据源创建器实例。 |
| dataSource | DataSource | 自动注入数据源实例。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| checkDbCode | long | 检查数据库代码是否存在，返回匹配记录数。 |
| removeDynamicDataSource | void | 移除指定代码的动态数据源。 |
| deleteDataSource | Result | 删除数据源方法：根据ID获取数据源，清除缓存并删除记录，返回成功提示。 |
| editDataSource | Result | 编辑数据源方法：更新密码、移除缓存、返回成功。 |
| addDynamicDataSource | void | 动态添加数据源，配置URL、密码、驱动和用户名，并加入路由数据源。 |
| saveDataSource | Result | 保存数据源前检查编码，加密密码，成功后返回添加成功。 |




