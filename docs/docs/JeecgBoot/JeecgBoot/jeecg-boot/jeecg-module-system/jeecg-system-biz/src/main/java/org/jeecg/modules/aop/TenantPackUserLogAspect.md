# 基础信息

|      |      |
|------|------|
| 名称 | TenantPackUserLogAspect |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/aop/TenantPackUserLogAspect.java |
| 包名 | org.jeecg.modules.aop |
| 依赖项 | ['org.apache.shiro.SecurityUtils', 'org.aspectj.lang.ProceedingJoinPoint', 'org.aspectj.lang.annotation.AfterThrowing', 'org.aspectj.lang.annotation.Around', 'org.aspectj.lang.annotation.Aspect', 'org.aspectj.lang.annotation.Pointcut', 'org.aspectj.lang.reflect.MethodSignature', 'org.jeecg.common.api.dto.LogDTO', 'org.jeecg.common.constant.CommonConstant', 'org.jeecg.common.system.vo.LoginUser', 'org.jeecg.modules.base.service.BaseCommonService', 'org.jeecg.modules.system.entity.SysTenantPack', 'org.jeecg.modules.system.entity.SysTenantPackUser', 'org.springframework.stereotype.Component', 'javax.annotation.Resource', 'java.lang.reflect.Method', 'java.util.Date'] |
| 概述说明 | TenantPackUserLogAspect类记录租户操作日志，处理角色权限增删改。 |

# 说明

TenantPackUserLogAspect类主要用于记录租户的操作日志，涉及创建、添加和移除角色权限等关键操作。该类通过捕捉和处理这些操作，确保对租户行为的全面跟踪和记录，从而提供操作审计和日志管理的功能。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| TenantPackUserLogAspect | class | TenantPackUserLogAspect类用于记录租户操作日志，处理创建、添加和移除角色权限等操作。 |



## 类 TenantPackUserLogAspect

|      |      |
|------|------|
| 访问范围 | @Aspect;@Component;public |
| 类型 | class |
| 名称 | TenantPackUserLogAspect |
| 说明 | TenantPackUserLogAspect类用于记录租户操作日志，处理创建、添加和移除角色权限等操作。 |


### UML类图

```mermaid
classDiagram
    class TenantPackUserLogAspect {
        -BaseCommonService baseCommonService
        +tenantLogPointCut() void
        +aroundMethod(ProceedingJoinPoint joinPoint) Object
        +afterThrowing() void
    }

    class BaseCommonService {
        <<Interface>>
        +addLog(LogDTO dto) void
    }

    class LogDTO {
        -Integer logType
        -String logContent
        -Integer operateType
        -Integer tenantId
        -String userid
        -String username
        -Date createTime
        +setLogType(Integer logType) void
        +setLogContent(String logContent) void
        +setOperateType(Integer operateType) void
        +setTenantId(Integer tenantId) void
        +setUserid(String userid) void
        +setUsername(String username) void
        +setCreateTime(Date createTime) void
    }

    class SysTenantPack {
        -String packName
        -Integer tenantId
        +getPackName() String
        +getTenantId() Integer
    }

    class SysTenantPackUser {
        -String packName
        -String realname
        -Integer tenantId
        +getPackName() String
        +getRealname() String
        +getTenantId() Integer
    }

    class LoginUser {
        -String username
        -String realname
        +getUsername() String
        +getRealname() String
    }

    TenantPackUserLogAspect --> BaseCommonService : 依赖
    TenantPackUserLogAspect --> LogDTO : 依赖
    TenantPackUserLogAspect --> SysTenantPack : 依赖
    TenantPackUserLogAspect --> SysTenantPackUser : 依赖
    TenantPackUserLogAspect --> LoginUser : 依赖
```

**描述：**  
`TenantPackUserLogAspect` 是一个切面类，用于处理与租户操作相关的日志记录。它依赖于 `BaseCommonService` 接口来保存日志，并使用了 `LogDTO` 类来封装日志信息。在 `aroundMethod` 方法中，根据传入的参数类型（`SysTenantPack` 或 `SysTenantPackUser`），生成相应的日志内容，并通过 `BaseCommonService` 保存日志。`afterThrowing` 方法用于处理异常情况。


### 内部方法调用关系图

```mermaid
graph TD
    A["类TenantPackUserLogAspect"]
    B["属性: BaseCommonService baseCommonService"]
    C["切点: tenantLogPointCut()"]
    D["环绕通知: aroundMethod(ProceedingJoinPoint joinPoint)"]
    E["异常通知: afterThrowing()"]
    F["获取方法签名: MethodSignature signature = (MethodSignature) joinPoint.getSignature()"]
    G["获取方法: Method method = signature.getMethod()"]
    H["获取注解: TenantLog log = method.getAnnotation(TenantLog.class)"]
    I["判断注解是否存在: if(log != null)"]
    J["获取操作类型: int opType = log.value()"]
    K["初始化日志类型、内容、租户ID: Integer logType = null, String content = null, Integer tenantId = null"]
    L["获取方法参数: Object[] args = joinPoint.getArgs()"]
    M["判断参数是否为空: if(args.length>0)"]
    N["遍历参数: for(Object obj: args)"]
    O["判断参数类型: if(obj instanceof SysTenantPack)"]
    P["设置日志类型: logType = CommonConstant.LOG_TYPE_3"]
    Q["设置日志内容: content = '创建了角色权限 ' + pack.getPackName()"]
    R["获取租户ID: tenantId = pack.getTenantId()"]
    S["判断参数类型: if(obj instanceof SysTenantPackUser)"]
    T["设置日志类型: logType = CommonConstant.LOG_TYPE_3"]
    U["设置日志内容: content = '将 ' + packUser.getRealname() + ' 添加到角色 ' + packUser.getPackName()"]
    V["设置日志内容: content = '移除了 ' + packUser.getPackName() + ' 成员 ' + packUser.getRealname()"]
    W["获取租户ID: tenantId = packUser.getTenantId()"]
    X["判断日志类型是否为空: if(logType!=null)"]
    Y["创建日志DTO: LogDTO dto = new LogDTO()"]
    Z["设置日志类型: dto.setLogType(logType)"]
    AA["设置日志内容: dto.setLogContent(content)"]
    AB["设置操作类型: dto.setOperateType(opType)"]
    AC["设置租户ID: dto.setTenantId(tenantId)"]
    AD["获取登录用户信息: LoginUser sysUser = (LoginUser) SecurityUtils.getSubject().getPrincipal()"]
    AE["判断用户是否为空: if(sysUser!=null)"]
    AF["设置用户ID: dto.setUserid(sysUser.getUsername())"]
    AG["设置用户名: dto.setUsername(sysUser.getRealname())"]
    AH["设置创建时间: dto.setCreateTime(new Date())"]
    AI["保存系统日志: baseCommonService.addLog(dto)"]
    AJ["继续执行方法: return joinPoint.proceed()"]
    AK["输出异常通知: System.out.println('异常通知')"]

    A --> B
    A --> C
    A --> D
    A --> E
    D --> F
    F --> G
    G --> H
    H --> I
    I --> J
    I --> K
    I --> L
    L --> M
    M --> N
    N --> O
    O --> P
    O --> Q
    O --> R
    N --> S
    S --> T
    S --> U
    S --> V
    S --> W
    I --> X
    X --> Y
    Y --> Z
    Z --> AA
    AA --> AB
    AB --> AC
    AC --> AD
    AD --> AE
    AE --> AF
    AF --> AG
    AG --> AH
    AH --> AI
    I --> AJ
    E --> AK
```

这段代码是一个基于AOP（面向切面编程）的日志记录类，用于在特定方法执行前后记录租户操作日志。代码通过`@Around`注解在方法执行前后进行拦截，根据方法参数的类型和操作类型生成相应的日志内容，并通过`BaseCommonService`将日志保存到系统中。`@AfterThrowing`注解用于在方法抛出异常时执行异常通知。整体流程包括获取方法签名、解析注解、遍历参数、生成日志内容、保存日志等步骤。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| baseCommonService | BaseCommonService | 私有资源注入BaseCommonService实例。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| tenantLogPointCut | void | 定义切点，用于拦截带有TenantLog注解的方法。 |
| afterThrowing | void | 在切点抛出异常后执行异常通知。 |
| aroundMethod | Object | 环绕通知处理租户日志，根据操作类型记录日志并保存。 |




