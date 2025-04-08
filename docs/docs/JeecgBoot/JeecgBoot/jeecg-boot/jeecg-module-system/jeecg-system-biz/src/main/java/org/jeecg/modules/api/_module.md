# 基础信息

|      |      |
|------|------|
| 名称 | api |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/api |
| 包名 | JeecgBoot.jeecg-boot.jeecg-module-system.jeecg-system-biz.src.main.java.org.jeecg.modules.api |
| 概述说明 | SystemApiController支持消息发送、用户查询、字典和部门管理，处理多种模板和参数。 |

# 说明

SystemApiController是一个多功能接口控制器，提供系统消息发送、用户信息查询、字典管理和部门管理等功能。它支持处理多种消息模板和业务参数，确保系统的高效运行和灵活配置。


### 包内部结构视图

```mermaid
graph TD
    api --> controller
    controller --> SystemApiController.java
```

该流程图展示了JeecgBoot项目中模块系统的API路径结构。根节点为`api`，它包含一个`controller`子节点，而`controller`节点下又包含一个`SystemApiController.java`文件。这种层级关系清晰地反映了代码的组织方式，便于开发者理解和管理项目结构。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [controller](controller/_module.md) | package | SystemApiController支持消息发送、用户查询、字典和部门管理，处理多种模板和参数。 |


