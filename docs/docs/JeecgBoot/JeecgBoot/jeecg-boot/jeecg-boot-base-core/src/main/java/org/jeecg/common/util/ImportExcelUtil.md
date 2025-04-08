# 基础信息

|      |      |
|------|------|
| 名称 | ImportExcelUtil |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-boot-base-core/src/main/java/org/jeecg/common/util/ImportExcelUtil.java |
| 包名 | org.jeecg.common.util |
| 依赖项 | ['com.alibaba.fastjson.JSONObject', 'com.baomidou.mybatisplus.extension.service.IService', 'lombok.extern.slf4j.Slf4j', 'org.jeecg.common.api.vo.Result', 'org.jeecg.common.constant.CommonConstant', 'java.io.File', 'java.io.IOException', 'java.util.List'] |
| 概述说明 | 导入Excel工具类，处理数据及错误信息。 |

# 说明

该描述涉及一个Excel工具类，主要用于处理数据导入过程中的结果和错误信息。该工具类的主要功能是导入Excel文件，并对导入的数据进行解析和验证，确保数据的准确性和完整性。在处理过程中，工具类能够捕获并记录任何可能出现的错误信息，如格式错误、数据缺失或数据类型不匹配等。通过这些功能，工具类帮助用户高效地管理和修复数据导入过程中遇到的问题，确保数据能够顺利导入并应用于后续的业务流程中。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| ImportExcelUtil | class | 导入Excel工具类，处理数据导入结果和错误信息。 |



## 类 ImportExcelUtil

|      |      |
|------|------|
| 访问范围 | @Slf4j;public |
| 类型 | class |
| 名称 | ImportExcelUtil |
| 说明 | 导入Excel工具类，处理数据导入结果和错误信息。 |


### UML类图

```mermaid
classDiagram
    class ImportExcelUtil {
        +Result<?> imporReturnRes(int errorLines, int successLines, List~String~ errorMessage) throws IOException
        +List~String~ importDateSave(List~?~ list, Class serviceClass, List~String~ errorMessage, String errorFlag)
        +List~String~ importDateSaveOne(Object obj, Class serviceClass, List~String~ errorMessage, int i, String errorFlag)
    }

    class Result~T~ {
        +Result~T~ ok(T data)
        +void setCode(int code)
        +void setMessage(String message)
    }

    class IService {
        <<Interface>>
        +boolean save(Object obj)
    }

    class SpringContextUtils {
        +Object getBean(Class clazz)
    }

    ImportExcelUtil --> Result : 依赖
    ImportExcelUtil --> IService : 依赖
    ImportExcelUtil --> SpringContextUtils : 依赖
```

**描述：**  
`ImportExcelUtil` 类提供了三个静态方法，用于处理Excel导入操作。`imporReturnRes` 方法根据导入的成功和错误行数生成结果对象；`importDateSave` 方法批量保存导入数据，并捕获异常信息；`importDateSaveOne` 方法处理单个对象的保存，并记录错误信息。该类依赖于 `Result` 类返回操作结果，使用 `IService` 接口进行数据保存，并通过 `SpringContextUtils` 获取服务实例。


### 内部方法调用关系图

```mermaid
graph TD
    A["类ImportExcelUtil"]
    B["方法: Result<?> imporReturnRes(int errorLines, int successLines, List<String> errorMessage)"]
    C["方法: List<String> importDateSave(List<?> list, Class serviceClass, List<String> errorMessage, String errorFlag)"]
    D["方法: List<String> importDateSaveOne(Object obj, Class serviceClass, List<String> errorMessage, int i, String errorFlag)"]
    E["条件: errorLines == 0"]
    F["返回: Result.ok('共' + successLines + '行数据全部导入成功！')"]
    G["创建: JSONObject result"]
    H["计算: totalCount = successLines + errorLines"]
    I["设置: result.put('totalCount', totalCount)"]
    J["设置: result.put('errorCount', errorLines)"]
    K["设置: result.put('successCount', successLines)"]
    L["设置: result.put('msg', '总上传行数：' + totalCount + '，已导入行数：' + successLines + '，错误行数：' + errorLines)"]
    M["保存: fileUrl = PmsUtil.saveErrorTxtByList(errorMessage, 'userImportExcelErrorLog')"]
    N["获取: fileName = fileUrl.substring(lastIndex + 1)"]
    O["设置: result.put('fileUrl', '/sys/common/static/' + fileUrl)"]
    P["设置: result.put('fileName', fileName)"]
    Q["创建: Result res = Result.ok(result)"]
    R["设置: res.setCode(201)"]
    S["设置: res.setMessage('文件导入成功，但有错误。')"]
    T["返回: res"]
    U["获取: IService bean = SpringContextUtils.getBean(serviceClass)"]
    V["循环: for (int i = 0; i < list.size(); i++)"]
    W["尝试: boolean save = bean.save(list.get(i))"]
    X["条件: !save"]
    Y["抛出: throw new Exception(errorFlag)"]
    Z["捕获: catch (Exception e)"]
    AA["获取: message = e.getMessage().toLowerCase()"]
    AB["计算: lineNumber = i + 1"]
    AC["条件: message.contains(CommonConstant.SQL_INDEX_UNIQ_SYS_ROLE_CODE)"]
    AD["添加: errorMessage.add('第 ' + lineNumber + ' 行：角色编码已经存在，忽略导入。')"]
    AE["条件: message.contains(CommonConstant.SQL_INDEX_UNIQ_JOB_CLASS_NAME)"]
    AF["添加: errorMessage.add('第 ' + lineNumber + ' 行：任务类名已经存在，忽略导入。')"]
    AG["条件: message.contains(CommonConstant.SQL_INDEX_UNIQ_CODE)"]
    AH["添加: errorMessage.add('第 ' + lineNumber + ' 行：职务编码已经存在，忽略导入。')"]
    AI["条件: message.contains(CommonConstant.SQL_INDEX_UNIQ_DEPART_ORG_CODE)"]
    AJ["添加: errorMessage.add('第 ' + lineNumber + ' 行：部门编码已经存在，忽略导入。')"]
    AK["添加: errorMessage.add('第 ' + lineNumber + ' 行：未知错误，忽略导入')"]
    AL["记录: log.error(e.getMessage(), e)"]
    AM["返回: errorMessage"]
    AN["获取: IService bean = SpringContextUtils.getBean(serviceClass)"]
    AO["尝试: boolean save = bean.save(obj)"]
    AP["条件: !save"]
    AQ["抛出: throw new Exception(errorFlag)"]
    AR["捕获: catch (Exception e)"]
    AS["获取: message = e.getMessage().toLowerCase()"]
    AT["计算: lineNumber = i + 1"]
    AU["条件: message.contains(CommonConstant.SQL_INDEX_UNIQ_SYS_ROLE_CODE)"]
    AV["添加: errorMessage.add('第 ' + lineNumber + ' 行：角色编码已经存在，忽略导入。')"]
    AW["条件: message.contains(CommonConstant.SQL_INDEX_UNIQ_JOB_CLASS_NAME)"]
    AX["添加: errorMessage.add('第 ' + lineNumber + ' 行：任务类名已经存在，忽略导入。')"]
    AY["条件: message.contains(CommonConstant.SQL_INDEX_UNIQ_CODE)"]
    AZ["添加: errorMessage.add('第 ' + lineNumber + ' 行：职务编码已经存在，忽略导入。')"]
    BA["条件: message.contains(CommonConstant.SQL_INDEX_UNIQ_DEPART_ORG_CODE)"]
    BB["添加: errorMessage.add('第 ' + lineNumber + ' 行：部门编码已经存在，忽略导入。')"]
    BC["添加: errorMessage.add('第 ' + lineNumber + ' 行：未知错误，忽略导入')"]
    BD["记录: log.error(e.getMessage(), e)"]
    BE["返回: errorMessage"]

    A --> B
    A --> C
    A --> D
    B --> E
    E -->|是| F
    E -->|否| G
    G --> H
    H --> I
    I --> J
    J --> K
    K --> L
    L --> M
    M --> N
    N --> O
    O --> P
    P --> Q
    Q --> R
    R --> S
    S --> T
    C --> U
    U --> V
    V --> W
    W --> X
    X -->|是| Y
    X -->|否| Z
    Z --> AA
    AA --> AB
    AB --> AC
    AC -->|是| AD
    AC -->|否| AE
    AE -->|是| AF
    AE -->|否| AG
    AG -->|是| AH
    AG -->|否| AI
    AI -->|是| AJ
    AI -->|否| AK
    AK --> AL
    AL --> AM
    D --> AN
    AN --> AO
    AO --> AP
    AP -->|是| AQ
    AP -->|否| AR
    AR --> AS
    AS --> AT
    AT --> AU
    AU -->|是| AV
    AU -->|否| AW
    AW -->|是| AX
    AW -->|否| AY
    AY -->|是| AZ
    AY -->|否| BA
    BA -->|是| BB
    BA -->|否| BC
    BC --> BD
    BD --> BE
```

这段代码是一个用于处理Excel导入的工具类，包含三个主要方法。`imporReturnRes`方法根据导入结果返回不同的响应信息，`importDateSave`和`importDateSaveOne`方法分别用于批量保存和单个保存导入的数据，并处理可能的错误信息。代码通过捕获异常并根据异常信息生成相应的错误提示，最终返回错误信息列表或导入结果。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| importDateSave | List<String> | 导入数据时检查重复编码并记录错误信息。 |
| importDateSaveOne | List<String> | 方法导入数据并处理错误，返回错误信息列表。 |
| imporReturnRes | Result<?> | 方法根据导入结果返回成功或包含错误信息的响应。 |




