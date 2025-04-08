# 基础信息

|      |      |
|------|------|
| 名称 | SensitiveDataAspect |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-boot-base-core/src/main/java/org/jeecg/common/desensitization/aspect/SensitiveDataAspect.java |
| 包名 | org.jeecg.common.desensitization.aspect |
| 依赖项 | ['lombok.extern.slf4j.Slf4j', 'org.aspectj.lang.ProceedingJoinPoint', 'org.aspectj.lang.annotation.Around', 'org.aspectj.lang.annotation.Aspect', 'org.aspectj.lang.annotation.Pointcut', 'org.aspectj.lang.reflect.MethodSignature', 'org.jeecg.common.desensitization.annotation.SensitiveDecode', 'org.jeecg.common.desensitization.annotation.SensitiveEncode', 'org.jeecg.common.desensitization.util.SensitiveInfoUtil', 'org.springframework.stereotype.Component', 'java.lang.reflect.Method', 'java.util.List'] |
| 概述说明 | SensitiveDataAspect类负责敏感数据的加密解密，通过切点和注解实现。 |

# 说明

SensitiveDataAspect类专门负责处理敏感数据的加密和解密操作。它通过切点和方法注解的方式实现功能，确保在特定方法执行前后自动进行数据的加密或解密处理。这种设计提高了代码的安全性和可维护性，使得敏感数据的保护更加高效和自动化。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| SensitiveDataAspect | class | SensitiveDataAspect类用于处理敏感数据加密解密操作，通过切点和方法注解实现。 |



## 类 SensitiveDataAspect

|      |      |
|------|------|
| 访问范围 | @Slf4j;@Aspect;@Component;public |
| 类型 | class |
| 名称 | SensitiveDataAspect |
| 说明 | SensitiveDataAspect类用于处理敏感数据加密解密操作，通过切点和方法注解实现。 |


### UML类图

```mermaid
classDiagram
    class SensitiveDataAspect {
        +sensitivePointCut() void
        +around(ProceedingJoinPoint point) Object
    }

    class ProceedingJoinPoint {
        <<Interface>>
        +proceed() Object
        +getSignature() Signature
    }

    class MethodSignature {
        <<Interface>>
        +getMethod() Method
    }

    class Method {
        +getAnnotation(Class~T~ annotationClass) T
    }

    class SensitiveEncode {
        +entity() Class
    }

    class SensitiveDecode {
        +entity() Class
    }

    class SensitiveInfoUtil {
        +handlerObject(Object obj, boolean isEncode) void
        +handleList(Object list, Class entity, boolean isEncode) void
        +handleNestedObject(Object obj, Class entity, boolean isEncode) void
    }

    SensitiveDataAspect --> ProceedingJoinPoint : 依赖
    SensitiveDataAspect --> MethodSignature : 依赖
    SensitiveDataAspect --> Method : 依赖
    SensitiveDataAspect --> SensitiveEncode : 依赖
    SensitiveDataAspect --> SensitiveDecode : 依赖
    SensitiveDataAspect --> SensitiveInfoUtil : 依赖
    MethodSignature --> Method : 依赖
```

### 描述
`SensitiveDataAspect` 类是一个切面类，用于处理敏感数据的加密和解密操作。它通过定义切点 `sensitivePointCut` 来拦截带有 `SensitiveEncode` 或 `SensitiveDecode` 注解的方法。在 `around` 方法中，它根据方法的返回类型和注解信息，调用 `SensitiveInfoUtil` 类中的相应方法进行数据处理。该类依赖于 `ProceedingJoinPoint`、`MethodSignature`、`Method`、`SensitiveEncode`、`SensitiveDecode` 和 `SensitiveInfoUtil` 等类来完成其功能。


### 内部方法调用关系图

```mermaid
graph TD
    A["类SensitiveDataAspect"]
    B["切点: sensitivePointCut()"]
    C["环绕通知: around(ProceedingJoinPoint point)"]
    D["执行目标方法: point.proceed()"]
    E["判断结果是否为null: if(result == null)"]
    F["获取结果类: Class resultClass = result.getClass()"]
    G["判断是否为基本类型: if(resultClass.isPrimitive())"]
    H["获取方法注解信息: MethodSignature methodSignature = (MethodSignature) point.getSignature()"]
    I["获取方法: Method method = methodSignature.getMethod()"]
    J["获取SensitiveEncode注解: SensitiveEncode encode = method.getAnnotation(SensitiveEncode.class)"]
    K["判断encode是否为null: if(encode==null)"]
    L["获取SensitiveDecode注解: SensitiveDecode decode = method.getAnnotation(SensitiveDecode.class)"]
    M["设置isEncode为false: isEncode = false"]
    N["设置entity: entity = decode.entity()"]
    O["设置entity: entity = encode.entity()"]
    P["判断结果类是否与entity一致: if(resultClass.equals(entity) || entity.equals(Object.class))"]
    Q["处理对象: SensitiveInfoUtil.handlerObject(result, isEncode)"]
    R["判断结果是否为List: if(result instanceof List)"]
    S["处理List: SensitiveInfoUtil.handleList(result, entity, isEncode)"]
    T["处理嵌套对象: SensitiveInfoUtil.handleNestedObject(result, entity, isEncode)"]
    U["记录耗时: log.info((isEncode ? '加密操作，' : '解密操作，') + 'Aspect程序耗时：' + (endTime - startTime) + 'ms')"]

    A --> B
    A --> C
    C --> D
    D --> E
    E -->|是| F
    E -->|否| C
    F --> G
    G -->|是| C
    G -->|否| H
    H --> I
    I --> J
    J --> K
    K -->|是| L
    L --> M
    L --> N
    K -->|否| O
    N --> P
    O --> P
    P -->|是| Q
    P -->|否| R
    R -->|是| S
    R -->|否| T
    Q --> U
    S --> U
    T --> U
```

**描述：**  
该流程图展示了`SensitiveDataAspect`类中`around`方法的执行流程。首先，方法通过`point.proceed()`执行目标方法并获取结果。接着，判断结果是否为null或基本类型，如果是则直接返回。否则，获取方法注解信息，判断是加密还是解密操作，并根据结果的类型（对象、List或嵌套对象）调用相应的处理方法。最后，记录操作耗时并返回结果。整个流程确保了敏感数据的正确处理和日志记录。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| sensitivePointCut | void | 切面方法，用于处理敏感数据编码和解码注解。 |
| around | Object | 该方法通过AOP处理敏感信息，判断加密或解密操作，并记录耗时。 |




