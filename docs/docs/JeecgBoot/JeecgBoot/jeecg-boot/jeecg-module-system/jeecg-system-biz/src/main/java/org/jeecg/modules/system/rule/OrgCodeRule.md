# 基础信息

|      |      |
|------|------|
| 名称 | OrgCodeRule |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/system/rule/OrgCodeRule.java |
| 包名 | org.jeecg.modules.system.rule |
| 依赖项 | ['com.alibaba.fastjson.JSONObject', 'com.baomidou.mybatisplus.core.conditions.query.LambdaQueryWrapper', 'com.baomidou.mybatisplus.core.metadata.IPage', 'com.baomidou.mybatisplus.extension.plugins.pagination.Page', 'io.netty.util.internal.StringUtil', 'org.jeecg.common.handler.IFillRuleHandler', 'org.jeecg.common.util.SpringContextUtils', 'org.jeecg.common.util.YouBianCodeUtil', 'org.jeecg.modules.system.entity.SysDepart', 'org.jeecg.modules.system.service.ISysDepartService', 'java.util.ArrayList', 'java.util.List'] |
| 概述说明 | OrgCodeRule类实现IFillRuleHandler接口，用于生成部门编码和类型。 |

# 说明

OrgCodeRule类实现了IFillRuleHandler接口，负责生成部门编码和类型。该类的主要功能是通过实现接口中的方法，确保能够按照特定规则生成符合要求的部门编码和类型信息。这一实现确保了编码生成的规范性和一致性，适用于需要自动生成部门编码的场景。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| OrgCodeRule | class | OrgCodeRule类实现IFillRuleHandler，生成部门编码和类型。 |



## 类 OrgCodeRule

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | OrgCodeRule |
| 说明 | OrgCodeRule类实现IFillRuleHandler，生成部门编码和类型。 |


### UML类图

```mermaid
classDiagram
    class OrgCodeRule {
        +execute(JSONObject params, JSONObject formData) Object
    }
    class IFillRuleHandler {
        <<Interface>>
        +execute(JSONObject params, JSONObject formData) Object
    }
    class ISysDepartService {
        <<Interface>>
        +getMaxCodeDepart(Page~SysDepart~ page, String parentId) IPage~SysDepart~
        +getDepartById(String parentId) SysDepart
    }
    class SysDepart {
        +String getOrgCode()
        +String getOrgType()
    }
    class YouBianCodeUtil {
        +getNextYouBianCode(String oldOrgCode) String
        +getSubYouBianCode(String parentCode, String subCode) String
    }
    class SpringContextUtils {
        +getBean(String beanName) Object
    }
    class LambdaQueryWrapper~T~ {
        +LambdaQueryWrapper()
    }
    class Page~T~ {
        +Page(int current, int size)
    }
    class IPage~T~ {
        +List~T~ getRecords()
    }
    class List~T~ {
        +size() int
        +get(int index) T
    }
    OrgCodeRule --> IFillRuleHandler : 实现
    OrgCodeRule --> ISysDepartService : 依赖
    OrgCodeRule --> YouBianCodeUtil : 依赖
    OrgCodeRule --> SpringContextUtils : 依赖
    ISysDepartService --> SysDepart : 依赖
    ISysDepartService --> Page~SysDepart~ : 依赖
    ISysDepartService --> IPage~SysDepart~ : 依赖
    ISysDepartService --> List~SysDepart~ : 依赖
    YouBianCodeUtil --> String : 依赖
    SpringContextUtils --> Object : 依赖
    LambdaQueryWrapper~SysDepart~ --> SysDepart : 依赖
    Page~SysDepart~ --> SysDepart : 依赖
    IPage~SysDepart~ --> SysDepart : 依赖
    List~SysDepart~ --> SysDepart : 依赖
```

这段代码定义了一个 `OrgCodeRule` 类，实现了 `IFillRuleHandler` 接口，用于生成部门编码。`OrgCodeRule` 类通过 `ISysDepartService` 接口与 `SysDepart` 类交互，获取部门信息，并使用 `YouBianCodeUtil` 工具类生成新的部门编码。`SpringContextUtils` 类用于从 Spring 上下文中获取 `ISysDepartService` 的实例。代码中使用了 `LambdaQueryWrapper`、`Page`、`IPage` 和 `List` 等泛型类来处理查询和分页逻辑。整体流程包括获取父级部门信息、生成新编码，并返回包含新编码和部门类型的数组。


### 内部方法调用关系图

```mermaid
graph TD
    A["execute(JSONObject params, JSONObject formData)"]
    B["初始化变量: ISysDepartService, LambdaQueryWrapper, List<SysDepart>, String[], String"]
    C["检查formData是否包含parentId"]
    D["检查params是否包含parentId"]
    E["判断parentId是否为空"]
    F["查询最大编码的部门信息"]
    G["判断查询结果是否为空"]
    H["生成初始编码并返回"]
    I["获取旧编码和部门类型"]
    J["生成新编码"]
    K["查询父级部门信息"]
    L["获取父级部门编码"]
    M["计算当前部门类型"]
    N["判断同级部门是否存在"]
    O["生成当前部门编码并返回"]
    P["生成同级部门编码并返回"]
    Q["返回最终编码和部门类型"]

    A --> B
    B --> C
    C -->|是| D
    C -->|否| E
    D --> E
    E -->|是| F
    E -->|否| K
    F --> G
    G -->|是| H
    G -->|否| I
    I --> J
    J --> Q
    K --> L
    L --> M
    M --> N
    N -->|是| P
    N -->|否| O
    O --> Q
    P --> Q
```

**描述：**  
该流程图描述了`OrgCodeRule`类中`execute`方法的执行流程。方法首先初始化变量并检查`formData`和`params`中是否包含`parentId`。根据`parentId`是否为空，分别查询最大编码的部门信息或父级部门信息。根据查询结果生成新的部门编码，并返回包含编码和部门类型的数组。流程图中详细展示了各个判断和生成编码的步骤，确保逻辑清晰且易于理解。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| execute | Object | 根据父部门ID生成新部门编码，返回编码和部门类型。 |




