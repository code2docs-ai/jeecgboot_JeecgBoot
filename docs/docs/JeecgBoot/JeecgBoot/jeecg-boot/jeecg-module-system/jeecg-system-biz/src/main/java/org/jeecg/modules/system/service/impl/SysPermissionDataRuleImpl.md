# 基础信息

|      |      |
|------|------|
| 名称 | SysPermissionDataRuleImpl |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/system/service/impl/SysPermissionDataRuleImpl.java |
| 包名 | org.jeecg.modules.system.service.impl |
| 依赖项 | ['java.util.HashSet', 'java.util.List', 'java.util.Set', 'javax.annotation.Resource', 'org.jeecg.common.constant.CommonConstant', 'org.jeecg.common.system.query.QueryGenerator', 'org.jeecg.common.util.oConvertUtils', 'org.jeecg.modules.system.entity.SysPermission', 'org.jeecg.modules.system.entity.SysPermissionDataRule', 'org.jeecg.modules.system.mapper.SysPermissionDataRuleMapper', 'org.jeecg.modules.system.mapper.SysPermissionMapper', 'org.jeecg.modules.system.service.ISysPermissionDataRuleService', 'org.springframework.stereotype.Service', 'org.springframework.transaction.annotation.Transactional', 'com.baomidou.mybatisplus.core.conditions.query.LambdaQueryWrapper', 'com.baomidou.mybatisplus.core.conditions.query.QueryWrapper', 'com.baomidou.mybatisplus.extension.service.impl.ServiceImpl'] |
| 概述说明 | SysPermissionDataRuleImpl类实现权限查询、保存、删除，支持菜单ID、权限名称和值查询，处理数据权限失效。 |

# 说明

SysPermissionDataRuleImpl类主要负责权限数据的管理，包括查询、保存和删除功能。该类支持根据菜单ID、权限名称和权限值进行数据查询，并能有效处理数据权限失效的问题，确保权限数据的准确性和有效性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| SysPermissionDataRuleImpl | class | SysPermissionDataRuleImpl类实现权限数据查询、保存、删除功能，支持按菜单ID、权限名称和值查询，并处理数据权限失效问题。 |



## 类 SysPermissionDataRuleImpl

|      |      |
|------|------|
| 访问范围 | @Service;public |
| 类型 | class |
| 名称 | SysPermissionDataRuleImpl |
| 说明 | SysPermissionDataRuleImpl类实现权限数据查询、保存、删除功能，支持按菜单ID、权限名称和值查询，并处理数据权限失效问题。 |


### UML类图

```mermaid
classDiagram
    class SysPermissionDataRuleImpl {
        -SysPermissionMapper sysPermissionMapper
        +List~SysPermissionDataRule~ getPermRuleListByPermId(String permissionId)
        +List~SysPermissionDataRule~ queryPermissionRule(SysPermissionDataRule permRule)
        +List~SysPermissionDataRule~ queryPermissionDataRules(String username, String permissionId)
        +void savePermissionDataRule(SysPermissionDataRule sysPermissionDataRule)
        +void deletePermissionDataRule(String dataRuleId)
    }

    class SysPermissionDataRule {
        // 假设该类包含权限数据的属性和方法
    }

    class SysPermission {
        // 假设该类包含权限的属性和方法
    }

    class SysPermissionMapper {
        +SysPermission selectById(String permissionId)
        +void updateById(SysPermission permission)
    }

    class ISysPermissionDataRuleService {
        <<Interface>>
        +List~SysPermissionDataRule~ getPermRuleListByPermId(String permissionId)
        +List~SysPermissionDataRule~ queryPermissionRule(SysPermissionDataRule permRule)
        +List~SysPermissionDataRule~ queryPermissionDataRules(String username, String permissionId)
        +void savePermissionDataRule(SysPermissionDataRule sysPermissionDataRule)
        +void deletePermissionDataRule(String dataRuleId)
    }

    SysPermissionDataRuleImpl --> SysPermissionMapper : 依赖
    SysPermissionDataRuleImpl --> ISysPermissionDataRuleService : 实现
    SysPermissionDataRuleImpl --> SysPermissionDataRule : 依赖
    SysPermissionDataRuleImpl --> SysPermission : 依赖
```

**描述**：  
`SysPermissionDataRuleImpl` 类实现了 `ISysPermissionDataRuleService` 接口，提供了权限数据规则的查询、保存和删除功能。该类依赖于 `SysPermissionMapper` 来操作权限数据，并处理与 `SysPermissionDataRule` 和 `SysPermission` 相关的业务逻辑。通过 `@Transactional` 注解，确保在保存和删除操作中的事务一致性。该类的核心功能包括根据菜单ID查询权限数据、根据权限名称和值查询权限数据、以及处理权限数据的保存和删除。


### 内部方法调用关系图

```mermaid
graph TD
    A["类SysPermissionDataRuleImpl"]
    B["属性: SysPermissionMapper sysPermissionMapper"]
    C["方法: List<SysPermissionDataRule> getPermRuleListByPermId(String permissionId)"]
    D["方法: List<SysPermissionDataRule> queryPermissionRule(SysPermissionDataRule permRule)"]
    E["方法: List<SysPermissionDataRule> queryPermissionDataRules(String username, String permissionId)"]
    F["方法: void savePermissionDataRule(SysPermissionDataRule sysPermissionDataRule)"]
    G["方法: void deletePermissionDataRule(String dataRuleId)"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G

    C --> H["创建LambdaQueryWrapper<SysPermissionDataRule>"]
    H --> I["设置查询条件: eq(SysPermissionDataRule::getPermissionId, permissionId)"]
    I --> J["设置排序条件: orderByDesc(SysPermissionDataRule::getCreateTime)"]
    J --> K["执行查询: this.list(query)"]
    K --> L["返回查询结果: permRuleList"]

    D --> M["初始化QueryWrapper: QueryGenerator.initQueryWrapper(permRule, null)"]
    M --> N["执行查询: this.list(queryWrapper)"]
    N --> O["返回查询结果"]

    E --> P["查询数据规则ID: this.baseMapper.queryDataRuleIds(username, permissionId)"]
    P --> Q["检查idsList是否为空"]
    Q --> R["遍历idsList, 处理并收集有效ID"]
    R --> S["检查set是否为空"]
    S --> T["执行查询: this.baseMapper.selectList(new QueryWrapper<SysPermissionDataRule>().in('id', set).eq('status', CommonConstant.STATUS_1))"]
    T --> U["返回查询结果"]

    F --> V["保存权限数据规则: this.save(sysPermissionDataRule)"]
    V --> W["查询权限: sysPermissionMapper.selectById(sysPermissionDataRule.getPermissionId)"]
    W --> X["检查权限是否存在且RuleFlag为0"]
    X --> Y["更新权限RuleFlag为1: sysPermissionMapper.updateById(permission)"]

    G --> Z["查询数据规则: this.baseMapper.selectById(dataRuleId)"]
    Z --> AA["删除数据规则: this.removeById(dataRuleId)"]
    AA --> AB["查询剩余数据规则数量: this.baseMapper.selectCount(new LambdaQueryWrapper<SysPermissionDataRule>().eq(SysPermissionDataRule::getPermissionId, dataRule.getPermissionId))"]
    AB --> AC["检查数量是否为0"]
    AC --> AD["更新权限RuleFlag为0: sysPermissionMapper.updateById(permission)"]
```

**描述：**
该流程图展示了`SysPermissionDataRuleImpl`类的主要方法及其内部逻辑。类中包含多个方法，用于处理权限数据规则的查询、保存和删除操作。每个方法都通过一系列步骤完成其功能，如创建查询条件、执行查询、处理结果等。流程图清晰地展示了这些方法的调用关系和数据流动，帮助理解代码的执行流程和逻辑结构。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| sysPermissionMapper | SysPermissionMapper | 定义私有SysPermissionMapper资源对象。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| deletePermissionDataRule | void | 删除权限数据规则，检查并更新权限标志。 |
| queryPermissionRule | List<SysPermissionDataRule> | 该方法查询权限规则，使用查询包装器并返回结果列表。 |
| getPermRuleListByPermId | List<SysPermissionDataRule> | 根据权限ID查询并返回按创建时间降序排列的权限规则列表。 |
| queryPermissionDataRules | List<SysPermissionDataRule> | 该方法查询用户权限数据规则，处理空值并返回有效规则列表。 |
| savePermissionDataRule | void | 保存权限数据规则并更新权限标志。 |




