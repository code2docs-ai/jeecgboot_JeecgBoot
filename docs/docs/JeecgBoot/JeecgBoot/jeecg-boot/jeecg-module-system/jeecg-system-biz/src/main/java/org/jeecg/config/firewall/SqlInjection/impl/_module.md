# 基础信息

|      |      |
|------|------|
| 名称 | impl |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/config/firewall/SqlInjection/impl |
| 包名 | JeecgBoot.jeecg-boot.jeecg-module-system.jeecg-system-biz.src.main.java.org.jeecg.config.firewall.SqlInjection.impl |
| 概述说明 | 实现SQL和字典查询的白名单校验，自动添加dev模式数据。 |

# 说明

该功能实现了表字典白名单校验，支持通过SQL查询和字典查询两种方式进行验证。系统能够自动在开发模式下添加白名单数据，确保在开发和测试环境中数据的合法性和安全性。这一机制有助于提高数据校验的灵活性和效率，同时简化了开发过程中的配置操作。


### 包内部结构视图

```mermaid
graph TD
    impl --> DictTableWhiteListHandlerImpl.java
```

该流程图展示了路径的层级关系，`impl` 文件夹包含了一个名为 `DictTableWhiteListHandlerImpl.java` 的文件。这种结构表示 `impl` 是父目录，而 `DictTableWhiteListHandlerImpl.java` 是其子文件，用于处理字典表白名单的逻辑。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [DictTableWhiteListHandlerImpl.java](DictTableWhiteListHandlerImpl.md) | file | 实现SQL和字典查询的白名单校验，自动添加dev模式数据。 |


