# 基础信息

|      |      |
|------|------|
| 名称 | PushMsgUtil |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/message/util/PushMsgUtil.java |
| 包名 | org.jeecg.modules.message.util |
| 依赖项 | ['freemarker.template.Configuration', 'freemarker.template.Template', 'freemarker.template.TemplateException', 'org.jeecg.modules.message.entity.SysMessage', 'org.jeecg.modules.message.entity.SysMessageTemplate', 'org.jeecg.modules.message.handle.enums.SendMsgStatusEnum', 'org.jeecg.modules.message.service.ISysMessageService', 'org.jeecg.modules.message.service.ISysMessageTemplateService', 'org.springframework.beans.factory.annotation.Autowired', 'org.springframework.stereotype.Component', 'com.alibaba.fastjson.JSONObject', 'java.io.IOException', 'java.io.StringWriter', 'java.util.Date', 'java.util.List', 'java.util.Map'] |
| 概述说明 | PushMsgUtil类通过模板发送短信、邮件和微信，处理内容并保存记录。 |

# 说明

PushMsgUtil类是一个用于通过模板发送消息的工具，支持短信、邮件和微信等多种消息类型。该类能够处理模板内容，确保消息格式正确，并自动保存发送记录，便于后续查询和管理。其功能全面，适用于多种消息发送场景，提高了消息发送的效率和可靠性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| PushMsgUtil | class | PushMsgUtil类通过模板发送消息，支持短信、邮件和微信，处理模板内容并保存消息记录。 |



## 类 PushMsgUtil

|      |      |
|------|------|
| 访问范围 | @Component;public |
| 类型 | class |
| 名称 | PushMsgUtil |
| 说明 | PushMsgUtil类通过模板发送消息，支持短信、邮件和微信，处理模板内容并保存消息记录。 |


### UML类图

```mermaid
classDiagram
    class PushMsgUtil {
        -ISysMessageService sysMessageService
        -ISysMessageTemplateService sysMessageTemplateService
        -Configuration freemarkerConfig
        +boolean sendMessage(String msgType, String templateCode, Map~String, String~ map, String sentTo)
    }

    class ISysMessageService {
        <<Interface>>
        +boolean save(SysMessage sysMessage)
    }

    class ISysMessageTemplateService {
        <<Interface>>
        +List~SysMessageTemplate~ selectByCode(String templateCode)
    }

    class SysMessage {
        -String esType
        -String esReceiver
        -String esTitle
        -String esContent
        -String esParam
        -Date esSendTime
        -String esSendStatus
        -int esSendNum
    }

    class SysMessageTemplate {
        -String templateName
        -String templateContent
    }

    PushMsgUtil --> ISysMessageService : 依赖
    PushMsgUtil --> ISysMessageTemplateService : 依赖
    PushMsgUtil --> Configuration : 依赖
    ISysMessageService --> SysMessage : 依赖
    ISysMessageTemplateService --> SysMessageTemplate : 依赖
```

**描述：**
`PushMsgUtil` 是一个消息推送工具类，依赖 `ISysMessageService` 和 `ISysMessageTemplateService` 接口来保存消息和获取消息模板。它使用 `Configuration` 来处理模板内容，并根据消息类型、模板代码、参数和接收方发送消息。如果消息保存成功，返回 `true`，否则返回 `false`。


### 内部方法调用关系图

```mermaid
graph TD
    A["类PushMsgUtil"]
    B["属性: ISysMessageService sysMessageService"]
    C["属性: ISysMessageTemplateService sysMessageTemplateService"]
    D["属性: Configuration freemarkerConfig"]
    E["方法: boolean sendMessage(String msgType, String templateCode, Map<String, String> map, String sentTo)"]
    F["调用: sysMessageTemplateService.selectByCode(templateCode)"]
    G["创建: SysMessage sysMessage = new SysMessage()"]
    H["判断: sysSmsTemplates.size() > 0"]
    I["获取: SysMessageTemplate sysSmsTemplate = sysSmsTemplates.get(0)"]
    J["设置: sysMessage.setEsType(msgType)"]
    K["设置: sysMessage.setEsReceiver(sentTo)"]
    L["获取: String title = sysSmsTemplate.getTemplateName()"]
    M["获取: String content = sysSmsTemplate.getTemplateContent()"]
    N["创建: StringWriter stringWriter = new StringWriter()"]
    O["创建: Template template = new Template('SysMessageTemplate', content, freemarkerConfig)"]
    P["处理: template.process(map, stringWriter)"]
    Q["异常处理: IOException e"]
    R["异常处理: TemplateException e"]
    S["更新: content = stringWriter.toString()"]
    T["设置: sysMessage.setEsTitle(title)"]
    U["设置: sysMessage.setEsContent(content)"]
    V["设置: sysMessage.setEsParam(JSONObject.toJSONString(map))"]
    W["设置: sysMessage.setEsSendTime(new Date())"]
    X["设置: sysMessage.setEsSendStatus(SendMsgStatusEnum.WAIT.getCode())"]
    Y["设置: sysMessage.setEsSendNum(0)"]
    Z["调用: sysMessageService.save(sysMessage)"]
    AA["返回: true"]
    AB["返回: false"]

    A --> B
    A --> C
    A --> D
    A --> E
    E --> F
    E --> G
    E --> H
    H --> I
    I --> J
    I --> K
    I --> L
    I --> M
    I --> N
    I --> O
    O --> P
    P --> Q
    P --> R
    P --> S
    S --> T
    S --> U
    S --> V
    S --> W
    S --> X
    S --> Y
    Y --> Z
    Z --> AA
    H --> AB
    Q --> AB
    R --> AB
```

这段代码定义了一个名为 `PushMsgUtil` 的类，用于发送不同类型的消息（短信、邮件、微信）。代码通过调用 `sysMessageTemplateService` 获取消息模板，并使用 FreeMarker 模板引擎处理消息内容。处理后的消息内容被保存到 `SysMessage` 对象中，并通过 `sysMessageService` 进行保存。整个流程包括模板获取、消息内容处理、消息对象设置和保存操作，最终返回操作是否成功的布尔值。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| sysMessageService | ISysMessageService | 自动注入系统消息服务实例。 |
| freemarkerConfig | Configuration | 使用Autowired注解自动注入Freemarker配置实例。 |
| sysMessageTemplateService | ISysMessageTemplateService | 自动注入系统消息模板服务实例。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| sendMessage | boolean | 方法根据模板生成并发送消息，处理异常并返回发送结果。 |




