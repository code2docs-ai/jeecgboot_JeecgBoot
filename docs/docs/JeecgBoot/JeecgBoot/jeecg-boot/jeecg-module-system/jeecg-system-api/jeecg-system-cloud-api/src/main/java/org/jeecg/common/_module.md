# 基础信息

|      |      |
|------|------|
| 名称 | common |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-api/jeecg-system-cloud-api/src/main/java/org/jeecg/common |
| 包名 | JeecgBoot.jeecg-boot.jeecg-module-system.jeecg-system-api.jeecg-system-cloud-api.src.main.java.org.jeecg.common |
| 概述说明 | SysBaseAPIFallbackFactory创建异常回退实例，增强系统容错。SysBaseAPIFallback处理消息发送失败，记录日志并返回空值。 |

# 说明

## 概述
该代码模块主要围绕系统基础API的容错机制展开，旨在增强系统在异常情况下的稳定性和可靠性。模块的核心组件包括`SysBaseAPIFallbackFactory`和`SysBaseAPIFallback`，它们共同实现了在系统基础API调用失败时的回退机制。`SysBaseAPIFallbackFactory`负责创建带有异常信息的回退实例，而`SysBaseAPIFallback`则处理具体的失败情况，并记录相关日志。通过这些设计，模块确保系统在遇到异常时仍能提供基本的服务或错误处理机制。

## 主要业务场景
1. **系统基础API调用失败时的回退处理**：当系统基础API调用失败时，`SysBaseAPIFallbackFactory`会生成一个包含异常信息的回退实例，确保系统在异常情况下仍能继续运行，并提供基本的服务或错误处理机制。
2. **系统消息发送失败的处理**：`SysBaseAPIFallback`类专门用于处理系统消息发送失败的情况，并在失败时记录相关日志，确保系统能够及时捕捉和处理此类异常。
3. **接口调用的容错机制**：在接口实现中，`SysBaseAPIFallback`的其他方法在调用时返回`null`或空值，确保不会产生意外的副作用或错误，从而提供一个可靠的备用机制。


### 包内部结构视图

```mermaid
graph TD
    common --> system
    system --> api
    api --> factory
    api --> ISysBaseAPI.java
    api --> fallback
    factory --> SysBaseAPIFallbackFactory.java
    fallback --> SysBaseAPIFallback.java
```

该流程图展示了`JeecgBoot`项目中`jeecg-system-cloud-api`模块的代码结构。`common`目录下包含`system`子目录，`system`下包含`api`目录，`api`目录下又分为`factory`、`ISysBaseAPI.java`和`fallback`三个部分。`factory`目录中包含`SysBaseAPIFallbackFactory.java`文件，`fallback`目录中包含`SysBaseAPIFallback.java`文件。整体结构清晰，层级分明。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [system](system/_module.md) | package | SysBaseAPIFallbackFactory创建异常回退实例，增强系统容错。SysBaseAPIFallback处理消息发送失败，记录日志并返回空值。 |


