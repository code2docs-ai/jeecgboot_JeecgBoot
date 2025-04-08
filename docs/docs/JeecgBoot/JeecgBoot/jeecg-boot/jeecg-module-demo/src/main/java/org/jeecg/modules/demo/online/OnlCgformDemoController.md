# 基础信息

|      |      |
|------|------|
| 名称 | OnlCgformDemoController |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-demo/src/main/java/org/jeecg/modules/demo/online/OnlCgformDemoController.java |
| 包名 | org.jeecg.modules.demo.online |
| 依赖项 | ['com.alibaba.fastjson.JSONArray', 'com.alibaba.fastjson.JSONObject', 'lombok.extern.slf4j.Slf4j', 'org.jeecg.common.api.vo.Result', 'org.jeecg.common.system.vo.DictModel', 'org.jeecg.common.util.oConvertUtils', 'org.springframework.web.bind.annotation.PostMapping', 'org.springframework.web.bind.annotation.RequestBody', 'org.springframework.web.bind.annotation.RequestMapping', 'org.springframework.web.bind.annotation.RestController', 'java.util.ArrayList', 'java.util.List'] |
| 概述说明 | OnlCgformDemoController负责表单增强，涵盖列表处理、校验及修改功能。 |

# 说明

OnlCgformDemoController负责处理表单的增强功能，主要包括对列表数据的处理以及表单数据的校验和修改。该控制器确保表单数据的准确性和完整性，通过校验机制防止错误数据进入系统，并支持对现有表单数据的修改操作。此外，它还处理与表单相关的列表数据，确保数据的有效管理和展示。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| OnlCgformDemoController | class | OnlCgformDemoController处理表单增强，包含列表数据处理和表单数据校验及修改功能。 |



## 类 OnlCgformDemoController

|      |      |
|------|------|
| 访问范围 | @Slf4j;@RestController("onlCgformDemoController");@RequestMapping("/demo/online/cgform");public |
| 类型 | class |
| 名称 | OnlCgformDemoController |
| 说明 | OnlCgformDemoController处理表单增强，包含列表数据处理和表单数据校验及修改功能。 |


### UML类图

```mermaid
classDiagram
    class OnlCgformDemoController {
        <<RestController>>
        +Result~?~ enhanceJavaListHttp(JSONObject params)
        +Result~?~ enhanceJavaHttp(JSONObject params)
        -List~DictModel~ virtualDictData()
    }

    class JSONObject {
        +String toJSONString()
        +JSONArray getJSONArray(String key)
        +JSONObject getJSONObject(String key)
        +String getString(String key)
        +void put(String key, Object value)
    }

    class JSONArray {
        +int size()
        +JSONObject getJSONObject(int index)
    }

    class DictModel {
        +String value
        +String text
        +DictModel(String value, String text)
        +String getValue()
        +String getText()
    }

    class Result~T~ {
        +static Result~T~ OK(T data)
        +static Result~T~ error(String message)
        +void setCode(int code)
    }

    OnlCgformDemoController --> JSONObject : 依赖
    OnlCgformDemoController --> JSONArray : 依赖
    OnlCgformDemoController --> DictModel : 依赖
    OnlCgformDemoController --> Result~?~ : 依赖
    JSONObject --> JSONArray : 依赖
    JSONArray --> JSONObject : 依赖
    DictModel --> Result~?~ : 依赖
```

### 描述
`OnlCgformDemoController` 是一个Spring Boot的RestController，提供了两个HTTP POST接口：`enhanceJavaListHttp` 和 `enhanceJavaHttp`。`enhanceJavaListHttp` 方法接收一个JSON对象，处理其中的数据列表，并根据字典数据更新省份名称。`enhanceJavaHttp` 方法接收一个JSON对象，进行表单数据的校验和处理，并返回处理结果。`virtualDictData` 方法模拟了一个字典数据列表。`JSONObject` 和 `JSONArray` 用于处理JSON数据，`DictModel` 表示字典数据模型，`Result` 是一个泛型类，用于封装返回结果。


### 内部方法调用关系图

```mermaid
graph TD
    A["类OnlCgformDemoController"]
    B["方法: enhanceJavaListHttp(JSONObject params)"]
    C["方法: virtualDictData()"]
    D["方法: enhanceJavaHttp(JSONObject params)"]
    E["日志: log.info(' --- params：' + params.toJSONString())"]
    F["获取数据: JSONArray dataList = params.getJSONArray('dataList')"]
    G["获取字典数据: List<DictModel> dict = virtualDictData()"]
    H["循环处理数据: for (int i = 0; i < dataList.size(); i++)"]
    I["获取记录: JSONObject record = dataList.getJSONObject(i)"]
    J["获取省份: String province = record.getString('province')"]
    K["判断省份是否为空: if (province == null)"]
    L["继续循环: continue"]
    M["过滤字典数据: dict.stream().filter(p -> province.equals(p.getValue()))"]
    N["映射文本: .map(DictModel::getText)"]
    O["获取结果: .findAny().orElse(province)"]
    P["更新记录: record.put('province', text)"]
    Q["返回结果: Result<?> res = Result.OK(dataList)"]
    R["设置返回码: res.setCode(1)"]
    S["返回结果: return res"]
    T["日志: log.info(' --- params：' + params.toJSONString())"]
    U["获取表名: String tableName = params.getString('tableName')"]
    V["获取记录: JSONObject record = params.getJSONObject('record')"]
    W["日志: log.info(' --- tableName：' + tableName)"]
    X["日志: log.info(' --- 行数据：' + record.toJSONString())"]
    Y["获取手机号: String phone = record.getString('phone')"]
    Z["判断手机号是否为空: if (oConvertUtils.isEmpty(phone))"]
    AA["返回错误: return Result.error('手机号不能为空！')"]
    AB["处理手机号: record.put('phone', '010-' + phone)"]
    AC["创建返回对象: JSONObject res = new JSONObject()"]
    AD["设置返回码: res.put('code', 1)"]
    AE["设置返回记录: res.put('record', record)"]
    AF["返回结果: return Result.OK(res)"]

    A --> B
    A --> C
    A --> D
    B --> E
    B --> F
    B --> G
    B --> H
    H --> I
    I --> J
    J --> K
    K --> L
    K --> M
    M --> N
    N --> O
    O --> P
    P --> Q
    Q --> R
    R --> S
    D --> T
    D --> U
    D --> V
    D --> W
    D --> X
    D --> Y
    Y --> Z
    Z --> AA
    Z --> AB
    D --> AC
    AC --> AD
    AD --> AE
    AE --> AF
```

**描述：**
该流程图展示了`OnlCgformDemoController`类中的主要方法及其调用关系。`enhanceJavaListHttp`方法接收JSON参数，处理数据列表，并通过字典数据更新省份信息，最终返回处理后的结果。`enhanceJavaHttp`方法接收JSON参数，处理表单数据，进行数据校验和处理，最终返回处理后的记录和状态码。流程图清晰地展示了每个方法的内部逻辑和调用顺序。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| virtualDictData | List<DictModel> | 生成包含北京、山东、安徽的虚拟字典数据列表。 |
| enhanceJavaListHttp | Result<?> | Java方法通过HTTP请求处理JSON数据，更新省份信息并返回结果。 |
| enhanceJavaHttp | Result<?> | Java HTTP接口处理表单数据，校验并修改后返回结果。 |




