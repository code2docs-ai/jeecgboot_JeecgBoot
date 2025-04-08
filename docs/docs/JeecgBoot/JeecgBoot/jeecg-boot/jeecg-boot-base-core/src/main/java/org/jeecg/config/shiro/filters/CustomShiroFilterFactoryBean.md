# 基础信息

|      |      |
|------|------|
| 名称 | CustomShiroFilterFactoryBean |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-boot-base-core/src/main/java/org/jeecg/config/shiro/filters/CustomShiroFilterFactoryBean.java |
| 包名 | org.jeecg.config.shiro.filters |
| 依赖项 | ['lombok.extern.slf4j.Slf4j', 'org.apache.shiro.spring.web.ShiroFilterFactoryBean', 'org.apache.shiro.web.filter.InvalidRequestFilter', 'org.apache.shiro.web.filter.mgt.DefaultFilter', 'org.apache.shiro.web.filter.mgt.FilterChainManager', 'org.apache.shiro.web.filter.mgt.FilterChainResolver', 'org.apache.shiro.web.filter.mgt.PathMatchingFilterChainResolver', 'org.apache.shiro.web.mgt.WebSecurityManager', 'org.apache.shiro.web.servlet.AbstractShiroFilter', 'org.apache.shiro.mgt.SecurityManager', 'org.springframework.beans.factory.BeanInitializationException', 'javax.servlet.Filter', 'java.util.Map'] |
| 概述说明 | 自定义Shiro过滤器工厂类，扩展并重写方法，确保安全配置正确。 |

# 说明

自定义Shiro过滤器工厂类通过扩展ShiroFilterFactoryBean，重写对象类型和实例创建方法，处理安全管理器和过滤器链解析器，确保安全配置正确。该方法通过自定义实现，增强了Shiro框架的灵活性和可扩展性，确保安全管理器和过滤器链的解析过程符合特定需求，从而提升系统的安全性和配置准确性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| CustomShiroFilterFactoryBean | class | 自定义Shiro过滤器工厂类，扩展ShiroFilterFactoryBean，重写对象类型和实例创建方法，处理安全管理器和过滤器链解析器，确保安全配置正确。 |



## 类 CustomShiroFilterFactoryBean

|      |      |
|------|------|
| 访问范围 | @Slf4j;public |
| 类型 | class |
| 名称 | CustomShiroFilterFactoryBean |
| 说明 | 自定义Shiro过滤器工厂类，扩展ShiroFilterFactoryBean，重写对象类型和实例创建方法，处理安全管理器和过滤器链解析器，确保安全配置正确。 |


### UML类图

```mermaid
classDiagram
    class CustomShiroFilterFactoryBean {
        +Class getObjectType()
        +AbstractShiroFilter createInstance() throws Exception
    }

    class MySpringShiroFilter {
        -WebSecurityManager webSecurityManager
        -FilterChainResolver resolver
        +MySpringShiroFilter(WebSecurityManager webSecurityManager, FilterChainResolver resolver)
    }

    class ShiroFilterFactoryBean {
        <<Interface>>
    }

    class AbstractShiroFilter {
        <<Interface>>
    }

    class WebSecurityManager {
        <<Interface>>
    }

    class FilterChainResolver {
        <<Interface>>
    }

    class PathMatchingFilterChainResolver {
        +void setFilterChainManager(FilterChainManager manager)
    }

    class FilterChainManager {
        <<Interface>>
        +Map~String, Filter~ getFilters()
    }

    class Filter {
        <<Interface>>
    }

    class InvalidRequestFilter {
        +void setBlockNonAscii(boolean blockNonAscii)
    }

    class DefaultFilter {
        <<Interface>>
    }

    CustomShiroFilterFactoryBean --> ShiroFilterFactoryBean : 继承
    CustomShiroFilterFactoryBean --> MySpringShiroFilter : 创建实例
    MySpringShiroFilter --> AbstractShiroFilter : 继承
    MySpringShiroFilter --> WebSecurityManager : 依赖
    MySpringShiroFilter --> FilterChainResolver : 依赖
    PathMatchingFilterChainResolver --> FilterChainManager : 依赖
    FilterChainManager --> Filter : 依赖
    InvalidRequestFilter --> Filter : 实现
    DefaultFilter --> Filter : 依赖
```

这段代码展示了`CustomShiroFilterFactoryBean`类如何继承`ShiroFilterFactoryBean`并重写`createInstance`方法，以创建一个自定义的`MySpringShiroFilter`实例。`MySpringShiroFilter`类继承自`AbstractShiroFilter`，并依赖于`WebSecurityManager`和`FilterChainResolver`接口。代码中还涉及到`PathMatchingFilterChainResolver`和`FilterChainManager`等组件，用于管理过滤器链和解析过滤器路径。通过这种方式，代码实现了对Shiro安全框架的扩展和定制。


### 内部方法调用关系图

```mermaid
graph TD
    A["类CustomShiroFilterFactoryBean"]
    B["重写方法: Class getObjectType()"]
    C["重写方法: AbstractShiroFilter createInstance()"]
    D["获取SecurityManager: getSecurityManager()"]
    E["检查SecurityManager是否为null"]
    F["抛出异常: BeanInitializationException('SecurityManager property must be set.')"]
    G["检查SecurityManager是否为WebSecurityManager"]
    H["抛出异常: BeanInitializationException('The security manager does not implement the WebSecurityManager interface.')"]
    I["创建FilterChainManager: createFilterChainManager()"]
    J["创建PathMatchingFilterChainResolver: new PathMatchingFilterChainResolver()"]
    K["设置FilterChainManager: chainResolver.setFilterChainManager(manager)"]
    L["获取FilterMap: manager.getFilters()"]
    M["获取InvalidRequestFilter: filterMap.get(DefaultFilter.invalidRequest.name())"]
    N["检查InvalidRequestFilter是否为InvalidRequestFilter"]
    O["设置blockNonAscii为false: ((InvalidRequestFilter) invalidRequestFilter).setBlockNonAscii(false)"]
    P["创建MySpringShiroFilter实例: new MySpringShiroFilter((WebSecurityManager) securityManager, chainResolver)"]
    Q["类MySpringShiroFilter"]
    R["构造方法: MySpringShiroFilter(WebSecurityManager webSecurityManager, FilterChainResolver resolver)"]
    S["检查webSecurityManager是否为null"]
    T["抛出异常: IllegalArgumentException('WebSecurityManager property cannot be null.')"]
    U["设置SecurityManager: this.setSecurityManager(webSecurityManager)"]
    V["检查resolver是否为null"]
    W["设置FilterChainResolver: this.setFilterChainResolver(resolver)"]

    A --> B
    A --> C
    C --> D
    D --> E
    E -- 是 --> F
    E -- 否 --> G
    G -- 是 --> H
    G -- 否 --> I
    I --> J
    J --> K
    K --> L
    L --> M
    M --> N
    N -- 是 --> O
    N -- 否 --> P
    P --> Q
    Q --> R
    R --> S
    S -- 是 --> T
    S -- 否 --> U
    U --> V
    V -- 是 --> W
```

这段代码展示了`CustomShiroFilterFactoryBean`类的实现，该类继承自`ShiroFilterFactoryBean`。代码主要重写了`getObjectType()`和`createInstance()`方法，用于创建和配置`MySpringShiroFilter`实例。在`createInstance()`方法中，首先获取并检查`SecurityManager`，然后创建`FilterChainManager`和`PathMatchingFilterChainResolver`，并对`InvalidRequestFilter`进行配置。最后，返回一个新的`MySpringShiroFilter`实例。`MySpringShiroFilter`是一个内部类，负责设置`SecurityManager`和`FilterChainResolver`。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| createInstance | AbstractShiroFilter | 创建ShiroFilter实例，检查SecurityManager，设置FilterChainResolver，跳过URL中文校验。 |
| getObjectType | Class | 重写getObjectType方法，返回MySpringShiroFilter类。 |




