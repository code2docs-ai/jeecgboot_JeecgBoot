# 基础信息

|      |      |
|------|------|
| 名称 | SystemSendMsgHandle |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/message/handle/impl/SystemSendMsgHandle.java |
| 包名 | org.jeecg.modules.message.handle.impl |
| 依赖项 | ['com.alibaba.fastjson.JSONObject', 'org.jeecg.common.api.dto.message.MessageDTO', 'org.jeecg.common.constant.CommonConstant', 'org.jeecg.common.constant.WebsocketConst', 'org.jeecg.common.exception.JeecgBootException', 'org.jeecg.common.system.api.ISysBaseAPI', 'org.jeecg.common.util.SpringContextUtils', 'org.jeecg.common.util.oConvertUtils', 'org.jeecg.common.constant.enums.Vue3MessageHrefEnum', 'org.jeecg.modules.message.handle.ISendMsgHandle', 'org.jeecg.modules.message.websocket.WebSocket', 'org.jeecg.modules.system.entity.SysAnnouncement', 'org.jeecg.modules.system.entity.SysAnnouncementSend', 'org.jeecg.modules.system.entity.SysUser', 'org.jeecg.modules.system.mapper.SysAnnouncementMapper', 'org.jeecg.modules.system.mapper.SysAnnouncementSendMapper', 'org.jeecg.modules.system.mapper.SysUserMapper', 'org.springframework.stereotype.Component', 'javax.annotation.Resource', 'java.util.Date', 'java.util.Map'] |
| 概述说明 | 系统消息处理类支持多平台消息发送，并记录发送状态。 |

# 说明

系统消息处理类实现了消息发送功能，支持通过系统、企业微信和钉钉等渠道发送消息，并能够记录每条消息的发送状态。该功能确保了消息的可靠传递和状态跟踪，适用于多种通信平台的需求。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| SystemSendMsgHandle | class | 系统消息处理类，实现消息发送功能，支持系统、企业微信、钉钉消息，并记录发送状态。 |



## 类 SystemSendMsgHandle

|      |      |
|------|------|
| 访问范围 | @Component("systemSendMsgHandle");public |
| 类型 | class |
| 名称 | SystemSendMsgHandle |
| 说明 | 系统消息处理类，实现消息发送功能，支持系统、企业微信、钉钉消息，并记录发送状态。 |


### UML类图

```mermaid
classDiagram
    class SystemSendMsgHandle {
        +String FROM_USER
        -SysAnnouncementMapper sysAnnouncementMapper
        -SysUserMapper userMapper
        -SysAnnouncementSendMapper sysAnnouncementSendMapper
        -WebSocket webSocket
        +sendMsg(String esReceiver, String esTitle, String esContent)
        +sendMessage(MessageDTO messageDTO)
        -doSend(String title, String msgContent, String fromUser, String toUser, Map~String, Object~ data)
    }

    class ISendMsgHandle {
        <<Interface>>
        +sendMsg(String esReceiver, String esTitle, String esContent)
        +sendMessage(MessageDTO messageDTO)
    }

    class SysAnnouncementMapper {
        +insert(SysAnnouncement announcement)
    }

    class SysUserMapper {
        +getUserByName(String username) SysUser
    }

    class SysAnnouncementSendMapper {
        +insert(SysAnnouncementSend announcementSend)
    }

    class WebSocket {
        +sendMessage(String userId, String message)
    }

    class MessageDTO {
        +String fromUser
        +String toUser
        +String title
        +String content
        +Map~String, Object~ data
    }

    class SysAnnouncement {
        +String titile
        +String msgContent
        +String sender
        +String priority
        +String msgType
        +String sendStatus
        +Date sendTime
        +String msgCategory
        +String delFlag
        +String msgAbstract
        +String busId
        +String busType
    }

    class SysAnnouncementSend {
        +String anntId
        +String userId
        +String readFlag
    }

    class SysUser {
        +String id
    }

    class JSONObject {
        +put(String key, Object value) JSONObject
        +toJSONString() String
    }

    SystemSendMsgHandle --> ISendMsgHandle : 实现
    SystemSendMsgHandle --> SysAnnouncementMapper : 依赖
    SystemSendMsgHandle --> SysUserMapper : 依赖
    SystemSendMsgHandle --> SysAnnouncementSendMapper : 依赖
    SystemSendMsgHandle --> WebSocket : 依赖
    SystemSendMsgHandle --> MessageDTO : 依赖
    SysAnnouncementMapper --> SysAnnouncement : 依赖
    SysUserMapper --> SysUser : 依赖
    SysAnnouncementSendMapper --> SysAnnouncementSend : 依赖
    WebSocket --> JSONObject : 依赖
```

**描述：**
`SystemSendMsgHandle` 类实现了 `ISendMsgHandle` 接口，负责处理系统消息的发送。它依赖于多个 Mapper 类（如 `SysAnnouncementMapper`、`SysUserMapper`、`SysAnnouncementSendMapper`）来操作数据库，并通过 `WebSocket` 发送实时消息。`sendMsg` 方法用于发送系统消息，而 `sendMessage` 方法则用于处理 `MessageDTO` 对象并调用 `doSend` 方法进行实际的消息发送。`doSend` 方法负责创建和插入 `SysAnnouncement` 和 `SysAnnouncementSend` 记录，并通过 `WebSocket` 发送消息给指定用户。


### 内部方法调用关系图

```mermaid
graph TD
    A["类SystemSendMsgHandle"]
    B["属性: SysAnnouncementMapper sysAnnouncementMapper"]
    C["属性: SysUserMapper userMapper"]
    D["属性: SysAnnouncementSendMapper sysAnnouncementSendMapper"]
    E["属性: WebSocket webSocket"]
    F["方法: sendMsg(String esReceiver, String esTitle, String esContent)"]
    G["方法: sendMessage(MessageDTO messageDTO)"]
    H["方法: doSend(String title, String msgContent, String fromUser, String toUser, Map<String, Object> data)"]
    I["检查: esReceiver是否为空"]
    J["异常: JeecgBootException('被发送人不能为空')"]
    K["获取: ISysBaseAPI sysBaseApi"]
    L["创建: MessageDTO messageDTO"]
    M["调用: sysBaseApi.sendSysAnnouncement(messageDTO)"]
    N["遍历: messageDTO.getToUser().split(',')"]
    O["调用: doSend(title, content, fromUser, username, data)"]
    P["创建: SysAnnouncement announcement"]
    Q["设置: announcement属性"]
    R["插入: sysAnnouncementMapper.insert(announcement)"]
    S["遍历: userId.split(',')"]
    T["获取: SysUser sysUser"]
    U["创建: SysAnnouncementSend announcementSend"]
    V["设置: announcementSend属性"]
    W["插入: sysAnnouncementSendMapper.insert(announcementSend)"]
    X["创建: JSONObject obj"]
    Y["设置: obj属性"]
    Z["调用: webSocket.sendMessage(sysUser.getId(), obj.toJSONString())"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    F --> I
    I -->|是| J
    I -->|否| K
    K --> L
    L --> M
    G --> N
    N --> O
    H --> P
    P --> Q
    Q --> R
    R --> S
    S --> T
    T --> U
    U --> V
    V --> W
    W --> X
    X --> Y
    Y --> Z
```

**描述**：该代码定义了一个名为`SystemSendMsgHandle`的类，负责处理系统消息的发送。类中包含两个主要方法：`sendMsg`和`sendMessage`，分别用于发送系统消息和处理消息DTO。`sendMsg`方法首先检查接收者是否为空，若为空则抛出异常，否则通过`ISysBaseAPI`发送系统公告。`sendMessage`方法遍历接收者列表，调用`doSend`方法发送消息。`doSend`方法创建并设置`SysAnnouncement`对象，插入数据库，并为每个接收者创建`SysAnnouncementSend`记录，最后通过WebSocket发送消息。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| FROM_USER="system" | String | 定义常量FROM_USER，值为"system"。 |
| sysAnnouncementSendMapper | SysAnnouncementSendMapper | 私有资源注入系统公告发送映射器。 |
| webSocket | WebSocket | 声明了一个私有的WebSocket资源变量。 |
| userMapper | SysUserMapper | 私有字段userMapper，类型为SysUserMapper。 |
| sysAnnouncementMapper | SysAnnouncementMapper | 私有成员变量sysAnnouncementMapper注入SysAnnouncementMapper类型。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| sendMsg | void | 方法发送消息，检查接收者非空，调用系统API发送公告。 |
| sendMessage | void | 重写sendMessage方法，拆分接收者并逐一发送消息。 |
| doSend | void | 发送系统公告并标记用户阅读状态，插入数据库并通知用户。 |




