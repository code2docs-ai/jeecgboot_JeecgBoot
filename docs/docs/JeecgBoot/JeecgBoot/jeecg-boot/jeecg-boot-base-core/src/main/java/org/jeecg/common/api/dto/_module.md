# 基础信息

|      |      |
|------|------|
| 名称 | dto |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-boot-base-core/src/main/java/org/jeecg/common/api/dto |
| 包名 | JeecgBoot.jeecg-boot.jeecg-boot-base-core.src.main.java.org.jeecg.common.api.dto |
| 概述说明 | FileUploadDTO处理文件上传，包含文件、路径、上传类型和存储桶属性。消息传输和模板管理模块通过多个DTO类封装消息信息，支持邮件推送和业务模板处理。DataLogDTO记录数据，包含表名、数据ID、内容、类型和创建者。OnlineAuthDTO支持在线认证，包含用户名、请求地址、表单地址和工单地址。FileDownDTO处理文件下载，包含文件路径、上传路径、上传类型和HTTP响应对象。LogDTO记录日志，包含内容、类型、操作、用户信息等。 |

# 说明

## 概述

该代码模块是一个多功能的数据传输和业务处理模块，涵盖了文件上传与下载、消息传输、模板管理、数据日志记录、在线认证以及日志管理等多个功能。模块通过多个数据传输对象（DTO）类来封装和传递不同业务场景下的数据，确保数据的完整性和一致性。核心类包括 `FileUploadDTO`、`FileDownDTO`、`MessageDTO`、`BusMessageDTO`、`TemplateDTO`、`TemplateMessageDTO`、`BusTemplateMessageDTO`、`DataLogDTO`、`OnlineAuthDTO` 和 `LogDTO`，它们分别用于处理文件操作、消息传输、模板管理、数据日志记录、在线认证以及日志管理。

## 主要业务场景

1. **文件上传与下载**：
   - `FileUploadDTO` 类用于处理文件上传操作，包含文件内容、上传路径、上传类型和自定义存储桶等属性，确保文件上传的统一管理和处理。
   - `FileDownDTO` 类用于处理文件下载操作，包含文件路径、上传路径、上传类型和HTTP响应对象等属性，确保文件下载功能的顺利实现。

2. **消息传输与模板管理**：
   - `MessageDTO` 类用于封装和传递消息的基本信息，支持邮件推送功能，确保消息能够通过多种渠道传递。
   - `BusMessageDTO` 类继承自 `MessageDTO`，新增了业务类型和业务ID两个属性，用于承载特定的业务信息。
   - `TemplateDTO` 类用于管理模板编码和参数，确保模板对象的完整性和一致性。
   - `TemplateMessageDTO` 类继承自 `TemplateDTO`，进一步扩展了消息相关的属性，支持序列化功能。
   - `BusTemplateMessageDTO` 类继承自 `TemplateMessageDTO`，主要用于处理业务相关的模板消息，新增了业务类型和业务ID两个字段。

3. **数据日志记录**：
   - `DataLogDTO` 类用于记录数据日志，包含表名、数据ID、内容、类型和创建者等字段，支持不同场景下的实例化需求。

4. **在线认证**：
   - `OnlineAuthDTO` 类用于在线认证，包含用户名、可能请求地址、online表单地址和工单地址等属性，支持序列化功能，确保数据在网络传输或存储时的完整性和一致性。

5. **日志管理**：
   - `LogDTO` 类用于记录日志信息，包含日志内容、日志类型、操作类型、用户信息、请求参数、请求路径、请求方法、用户账户信息、租户ID以及终端类型等字段，能够详细描述每一次操作的上下文信息，便于后续的日志分析和问题排查。

这些类共同构成了一个灵活且可扩展的数据传输和业务处理模块，适用于文件操作、消息传输、模板管理、数据日志记录、在线认证以及日志管理等多种业务场景。


### 包内部结构视图

```mermaid
graph TD
    dto --> FileUploadDTO.java
    dto --> message
    dto --> DataLogDTO.java
    dto --> OnlineAuthDTO.java
    dto --> FileDownDTO.java
    dto --> LogDTO.java
    message --> BusMessageDTO.java
    message --> MessageDTO.java
    message --> TemplateDTO.java
    message --> BusTemplateMessageDTO.java
    message --> TemplateMessageDTO.java
```

该流程图展示了`dto`目录下的层级结构，包括直接位于`dto`目录下的文件以及`message`子目录中的文件。`dto`目录下包含多个DTO文件，而`message`子目录中则进一步细分为多个与消息相关的DTO文件。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [DataLogDTO.java](DataLogDTO.md) | file | DataLogDTO类含表名、数据ID、内容、类型、创建者，支持多构造函数。 |
| [LogDTO.java](LogDTO.md) | file | LogDTO类包含日志内容、类型、操作、用户信息、请求参数等字段。 |
| [FileDownDTO.java](FileDownDTO.md) | file | FileDownDTO类用于文件下载，包含路径、类型和响应对象。 |
| [OnlineAuthDTO.java](OnlineAuthDTO.md) | file | OnlineAuthDTO类包含用户名、请求地址、表单地址和工单地址，支持序列化。 |
| [FileUploadDTO.java](FileUploadDTO.md) | file | FileUploadDTO类用于文件上传，包含文件、路径、类型和存储桶属性。 |
| [message](message/_module.md) | package | BusMessageDTO继承MessageDTO，新增业务类型和ID，支持业务信息传输。 |


