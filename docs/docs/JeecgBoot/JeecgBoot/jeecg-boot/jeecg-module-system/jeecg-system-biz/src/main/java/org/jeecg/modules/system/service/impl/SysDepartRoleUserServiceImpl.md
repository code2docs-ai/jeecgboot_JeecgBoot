# 基础信息

|      |      |
|------|------|
| 名称 | SysDepartRoleUserServiceImpl |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/system/service/impl/SysDepartRoleUserServiceImpl.java |
| 包名 | org.jeecg.modules.system.service.impl |
| 依赖项 | ['com.baomidou.mybatisplus.core.conditions.query.QueryWrapper', 'org.jeecg.common.util.oConvertUtils', 'org.jeecg.modules.system.entity.SysDepartRole', 'org.jeecg.modules.system.entity.SysDepartRoleUser', 'org.jeecg.modules.system.mapper.SysDepartRoleMapper', 'org.jeecg.modules.system.mapper.SysDepartRoleUserMapper', 'org.jeecg.modules.system.service.ISysDepartRoleUserService', 'org.springframework.beans.factory.annotation.Autowired', 'org.springframework.stereotype.Service', 'com.baomidou.mybatisplus.extension.service.impl.ServiceImpl', 'org.springframework.transaction.annotation.Transactional', 'java.util', 'java.util.stream.Collectors'] |
| 概述说明 | 实现部门角色用户管理，支持添加、移除及批量删除用户角色。 |

# 说明

实现部门角色用户管理功能，涵盖添加角色、移除角色以及批量删除用户角色等操作。该功能旨在优化部门内部角色分配与管理，提升用户权限控制的效率与灵活性。通过添加角色，可为用户分配特定权限；移除角色则可撤销用户的相关权限；批量删除用户角色功能则支持一次性处理多个用户的角色调整，简化管理流程。整体设计注重操作的便捷性与系统管理的全面性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| SysDepartRoleUserServiceImpl | class | 实现部门角色用户管理，包括添加、移除角色及批量删除用户角色功能。 |



## 类 SysDepartRoleUserServiceImpl

|      |      |
|------|------|
| 访问范围 | @Service;public |
| 类型 | class |
| 名称 | SysDepartRoleUserServiceImpl |
| 说明 | 实现部门角色用户管理，包括添加、移除角色及批量删除用户角色功能。 |


### UML类图

```mermaid
classDiagram
    class SysDepartRoleUserServiceImpl {
        -SysDepartRoleMapper sysDepartRoleMapper
        +void deptRoleUserAdd(String userId, String newRoleId, String oldRoleId)
        +void removeDeptRoleUser(List~String~ userIds, String depId)
        -List~String~ getDiff(String main, String diff)
    }

    class SysDepartRoleUserMapper {
    }

    class SysDepartRoleUser {
        +SysDepartRoleUser(String userId, String roleId)
        +String getUserId()
        +String getDroleId()
    }

    class SysDepartRole {
        +String getId()
    }

    class ISysDepartRoleUserService {
        <<Interface>>
        +void deptRoleUserAdd(String userId, String newRoleId, String oldRoleId)
        +void removeDeptRoleUser(List~String~ userIds, String depId)
    }

    class ServiceImpl~T~ {
    }

    class QueryWrapper~T~ {
        +QueryWrapper~T~ lambda()
        +QueryWrapper~T~ eq(String column, Object value)
        +QueryWrapper~T~ in(String column, List~String~ values)
    }

    SysDepartRoleUserServiceImpl --> SysDepartRoleUserMapper : 依赖
    SysDepartRoleUserServiceImpl --> SysDepartRoleUser : 依赖
    SysDepartRoleUserServiceImpl --> QueryWrapper~SysDepartRoleUser~ : 依赖
    SysDepartRoleUserServiceImpl --> ISysDepartRoleUserService : 实现
    SysDepartRoleUserServiceImpl --|> ServiceImpl~SysDepartRoleUser~ : 继承
    SysDepartRoleUserMapper --> SysDepartRole : 依赖
```

### 描述
`SysDepartRoleUserServiceImpl` 是一个服务实现类，继承自 `ServiceImpl` 并实现了 `ISysDepartRoleUserService` 接口。该类主要负责处理部门角色用户的添加和删除操作。它依赖于 `SysDepartRoleUserMapper` 进行数据库操作，并使用 `QueryWrapper` 构建查询条件。`getDiff` 方法用于比较两个字符串列表的差异。


### 内部方法调用关系图

```mermaid
graph TD
    A["类SysDepartRoleUserServiceImpl"]
    B["属性: SysDepartRoleMapper sysDepartRoleMapper"]
    C["方法: deptRoleUserAdd(String userId, String newRoleId, String oldRoleId)"]
    D["方法: removeDeptRoleUser(List<String> userIds, String depId)"]
    E["私有方法: getDiff(String main, String diff)"]
    F["步骤: 获取差异列表 add = getDiff(oldRoleId, newRoleId)"]
    G["步骤: 检查add列表是否为空且长度大于0"]
    H["步骤: 创建SysDepartRoleUser对象并添加到list"]
    I["步骤: 批量保存list"]
    J["步骤: 获取差异列表 remove = getDiff(newRoleId, oldRoleId)"]
    K["步骤: 检查remove列表是否为空且长度大于0"]
    L["步骤: 移除符合条件的记录"]
    M["步骤: 查询部门角色列表 sysDepartRoleList = sysDepartRoleMapper.selectList(...)"]
    N["步骤: 提取角色ID列表 roleIds = sysDepartRoleList.stream().map(...).collect(...)"]
    O["步骤: 检查roleIds列表是否为空且长度大于0"]
    P["步骤: 移除符合条件的记录"]
    Q["步骤: 检查diff是否为空"]
    R["步骤: 检查main是否为空"]
    S["步骤: 将main和diff拆分为数组"]
    T["步骤: 创建map并填充mainArr元素"]
    U["步骤: 遍历diffArr并找出不在map中的元素"]
    V["步骤: 返回结果列表 res"]

    A --> B
    A --> C
    A --> D
    A --> E
    C --> F
    C --> G
    G --> H
    G --> I
    C --> J
    C --> K
    K --> L
    D --> M
    D --> N
    D --> O
    O --> P
    E --> Q
    E --> R
    E --> S
    E --> T
    E --> U
    E --> V
```

这段代码是一个Spring Boot服务类，用于管理系统部门和角色用户的关系。它包含两个主要方法：`deptRoleUserAdd`用于添加和移除用户角色，`removeDeptRoleUser`用于移除部门角色用户。代码通过`getDiff`方法计算两个字符串的差异，并根据差异进行相应的操作。流程图中详细展示了各个方法的调用关系和步骤，确保代码逻辑清晰易懂。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| sysDepartRoleMapper | SysDepartRoleMapper | 自动注入SysDepartRoleMapper实例。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| removeDeptRoleUser | void | 删除部门角色用户，遍历用户ID，查询并移除相关角色。 |
| getDiff | List<String> | 比较两个字符串，返回差异项列表。 |
| deptRoleUserAdd | void | 方法实现用户角色更新，包括新增和删除角色操作。 |




