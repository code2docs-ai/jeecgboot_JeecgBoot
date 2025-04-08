# 基础信息

|      |      |
|------|------|
| 名称 | PmsUtil |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-boot-base-core/src/main/java/org/jeecg/common/util/PmsUtil.java |
| 包名 | org.jeecg.common.util |
| 依赖项 | ['lombok.extern.slf4j.Slf4j', 'org.springframework.beans.factory.annotation.Value', 'org.springframework.stereotype.Component', 'java.io.BufferedWriter', 'java.io.File', 'java.io.FileWriter', 'java.util.Date', 'java.util.List'] |
| 概述说明 | PmsUtil类用于保存错误日志，具备路径设置和日志文件生成功能。 |

# 说明

PmsUtil类主要用于错误日志的保存，具备路径设置和日志文件生成的功能。该类通过指定路径来存储日志文件，并能够自动生成日志文件以记录错误信息，确保系统运行中的问题能够被有效追踪和分析。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| PmsUtil | class | PmsUtil类用于保存错误日志，包含路径设置和日志文件生成功能。 |



## 类 PmsUtil

|      |      |
|------|------|
| 访问范围 | @Slf4j;@Component;public |
| 类型 | class |
| 名称 | PmsUtil |
| 说明 | PmsUtil类用于保存错误日志，包含路径设置和日志文件生成功能。 |


### UML类图

```mermaid
classDiagram
    class PmsUtil {
        -static String uploadPath
        +setUploadPath(String uploadPath) void
        +saveErrorTxtByList(List~String~ msg, String name) String
    }
```

```mermaid
flowchart TD
    A["开始"] --> B["获取当前日期"]
    B --> C["构建保存目录路径"]
    C --> D["检查目录是否存在"]
    D -- 不存在 --> E["创建目录"]
    D -- 存在 --> F["生成文件名"]
    E --> F
    F --> G["构建完整文件路径"]
    G --> H["创建BufferedWriter"]
    H --> I["遍历消息列表"]
    I --> J["检查消息是否包含'_'"]
    J -- 包含 --> K["分割消息并格式化写入"]
    J -- 不包含 --> L["直接写入消息"]
    K --> M["写入换行符"]
    L --> M
    M --> I
    I -- 遍历结束 --> N["释放BufferedWriter资源"]
    N --> O["返回文件路径"]
    O --> P["结束"]
    H -- 异常 --> Q["记录异常日志"]
    Q --> P
```

```mermaid
sequenceDiagram
    participant Client
    participant PmsUtil
    Client ->> PmsUtil: saveErrorTxtByList(List~String~ msg, String name)
    PmsUtil ->> PmsUtil: 获取当前日期
    PmsUtil ->> PmsUtil: 构建保存目录路径
    PmsUtil ->> PmsUtil: 检查目录是否存在
    PmsUtil ->> PmsUtil: 创建目录（如果不存在）
    PmsUtil ->> PmsUtil: 生成文件名
    PmsUtil ->> PmsUtil: 构建完整文件路径
    PmsUtil ->> PmsUtil: 创建BufferedWriter
    loop 遍历消息列表
        PmsUtil ->> PmsUtil: 检查消息是否包含'_'
        PmsUtil ->> PmsUtil: 分割消息并格式化写入（如果包含'_'）
        PmsUtil ->> PmsUtil: 直接写入消息（如果不包含'_'）
        PmsUtil ->> PmsUtil: 写入换行符
    end
    PmsUtil ->> PmsUtil: 释放BufferedWriter资源
    PmsUtil ->> Client: 返回文件路径
```

这段代码定义了一个名为 `PmsUtil` 的工具类，主要用于将错误信息列表保存到指定目录的文本文件中。代码首先通过 `setUploadPath` 方法设置上传路径，然后在 `saveErrorTxtByList` 方法中，根据当前日期生成保存目录，并检查目录是否存在，若不存在则创建。接着，生成唯一的文件名，并将错误信息逐行写入文本文件。如果消息中包含下划线 `_`，则将其分割并格式化写入，否则直接写入。最后，释放资源并返回文件路径。整个过程包含了异常处理，确保在发生异常时记录日志。


### 内部方法调用关系图

```mermaid
graph TD
    A["类PmsUtil"]
    B["静态属性: String uploadPath"]
    C["方法: setUploadPath(String uploadPath)"]
    D["方法: saveErrorTxtByList(List<String> msg, String name)"]
    E["创建日期对象: Date d = new Date()"]
    F["生成保存目录: String saveDir = 'logs' + File.separator + DateUtils.yyyyMMdd.get().format(d) + File.separator"]
    G["生成完整目录: String saveFullDir = uploadPath + File.separator + saveDir"]
    H["创建文件对象: File saveFile = new File(saveFullDir)"]
    I["检查目录是否存在: if (!saveFile.exists())"]
    J["创建目录: saveFile.mkdirs()"]
    K["生成文件名: name += DateUtils.yyyymmddhhmmss.get().format(d) + Math.round(Math.random() * 10000)"]
    L["生成完整文件路径: String saveFilePath = saveFullDir + name + '.txt'"]
    M["创建BufferedWriter对象: BufferedWriter bw = new BufferedWriter(new FileWriter(saveFilePath))"]
    N["遍历消息列表: for (String s : msg)"]
    O["检查消息格式: if (s.indexOf('_') > 0)"]
    P["拆分消息: String[] arr = s.split('_')"]
    Q["写入消息: bw.write('第' + arr[0] + '行:' + arr[1])"]
    R["写入消息: bw.write(s)"]
    S["写入换行符: bw.write('\\r\\n')"]
    T["刷新缓冲区: bw.flush()"]
    U["关闭BufferedWriter: bw.close()"]
    V["捕获异常: catch (Exception e)"]
    W["记录异常日志: log.info('excel导入生成错误日志文件异常:' + e.getMessage())"]
    X["返回文件路径: return saveDir + name + '.txt'"]

    A --> B
    A --> C
    A --> D
    D --> E
    D --> F
    D --> G
    D --> H
    D --> I
    I -->|是| J
    I -->|否| K
    D --> K
    D --> L
    D --> M
    D --> N
    N --> O
    O -->|是| P
    P --> Q
    O -->|否| R
    Q --> S
    R --> S
    S --> N
    D --> T
    D --> U
    D --> V
    V --> W
    D --> X
```

这段代码是一个用于保存错误日志的工具类，主要功能是将错误消息列表保存到指定的文本文件中。代码首先根据当前日期生成保存目录，然后创建文件并写入错误消息。如果消息中包含下划线，则将其拆分为行号和内容进行格式化写入。最后返回保存的文件路径。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| uploadPath | String | 定义静态字符串变量uploadPath。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| setUploadPath | void | 设置上传路径方法，将传入路径赋值给PmsUtil.uploadPath。 |
| saveErrorTxtByList | String | 该方法将错误信息列表保存为带时间戳的日志文件，返回文件路径。 |




