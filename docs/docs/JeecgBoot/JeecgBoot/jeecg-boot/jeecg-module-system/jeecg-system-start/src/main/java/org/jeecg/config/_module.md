# 基础信息

|      |      |
|------|------|
| 名称 | config |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-start/src/main/java/org/jeecg/config |
| 包名 | JeecgBoot.jeecg-boot.jeecg-module-system.jeecg-system-start.src.main.java.org.jeecg.config |
| 概述说明 | Flyway配置类支持MySQL数据库迁移，可设置脚本路径、编码、前缀、后缀等参数。 |

# 说明

Flyway配置类专为MySQL数据库迁移设计，提供多种参数设置功能，包括脚本路径、编码、前缀和后缀等。通过灵活配置这些参数，用户可以精确控制数据库迁移过程中的脚本加载和执行方式，确保迁移过程的高效性和准确性。


### 包内部结构视图

```mermaid
graph TD
    config --> flyway
    flyway --> FlywayConfig.java
```

该流程图展示了路径的层级关系，从`config`文件夹开始，包含`flyway`子文件夹，最终指向`FlywayConfig.java`文件。这种结构清晰地反映了项目配置模块的目录组织方式，方便开发者快速定位和理解相关文件的位置和关系。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [flyway](flyway/_module.md) | package | Flyway配置类支持MySQL数据库迁移，可设置脚本路径、编码、前缀、后缀等参数。 |


