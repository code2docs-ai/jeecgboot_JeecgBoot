# 基础信息

|      |      |
|------|------|
| 名称 | entity |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/system/entity |
| 包名 | JeecgBoot.jeecg-boot.jeecg-module-system.jeecg-system-biz.src.main.java.org.jeecg.modules.system.entity |
| 概述说明 | 各类实体类用于管理系统中的用户、角色、权限、部门、租户、日志等数据，确保数据的完整性、可追溯性和高效管理。 |

# 说明

## 概述
该代码模块是一个基于JeecgBoot框架的系统管理模块，涵盖了用户、角色、权限、部门、租户、产品包、数据源、日志、公告、字典、评论、文件管理等多个核心功能。模块通过多个实体类（如`SysUser`、`SysRole`、`SysPermission`、`SysDepart`等）实现了对系统基础数据的全面管理，支持多租户环境下的数据隔离与权限控制。模块还提供了对第三方系统集成、数据源管理、网关路由、填值规则等功能的支持，确保了系统的灵活性和可扩展性。

## 主要业务场景
1. **用户与权限管理**：通过`SysUser`、`SysRole`、`SysPermission`等类，模块实现了用户、角色、权限的精细化管理，支持用户与部门、角色、租户的关联，确保系统访问的安全性。
2. **租户与产品包管理**：`SysTenant`、`SysTenantPack`等类用于管理租户信息及其产品包，支持多租户环境下的资源配置与权限分配。
3. **部门与角色管理**：`SysDepart`、`SysDepartRole`等类用于组织内部部门与角色的管理，支持部门权限的细粒度控制。
4. **数据源与网关管理**：`SysDataSource`、`SysGatewayRoute`等类提供了多数据源配置和网关路由管理功能，支持系统的高效数据访问与流量控制。
5. **日志与监控**：`SysLog`、`SysDataLog`等类用于记录系统操作日志与数据变更，便于系统监控与问题排查。
6. **公告与评论管理**：`SysAnnouncement`、`SysComment`等类支持系统公告的发布与用户评论的管理，增强用户互动体验。
7. **字典与分类管理**：`SysDict`、`SysCategory`等类用于管理系统字典与分类数据，支持数据的标准化与规范化管理。
8. **第三方集成**：`SysThirdAccount`、`SysThirdAppConfig`等类支持第三方账号登录与系统集成，扩展系统的功能边界。
9. **文件与表单管理**：`SysFormFile`类用于管理表单评论中的文件信息，确保文件与数据的关联性与可追溯性。
10. **规则与配置管理**：`SysCheckRule`、`SysFillRule`等类用于定义和管理系统规则与配置，支持系统的灵活性与可定制性。

该模块通过丰富的实体类与功能设计，为复杂的企业级应用提供了全面的基础支持，适用于多租户、多角色、多数据源等复杂业务场景。


### 包内部结构视图

```mermaid
graph TD
    entity --> SysUserPosition.java
    entity --> SysTenantPackUser.java
    entity --> SysComment.java
    entity --> SysThirdAppConfig.java
    entity --> SysPermission.java
    entity --> SysDepartRolePermission.java
    entity --> SysUser.java
    entity --> SysTenant.java
    entity --> SysRolePermission.java
    entity --> SysPosition.java
    entity --> SysDepartRoleUser.java
    entity --> SysTableWhiteList.java
    entity --> SysDict.java
    entity --> SysCheckRule.java
    entity --> SysTenantPack.java
    entity --> SysRole.java
    entity --> SysAnnouncement.java
    entity --> SysDepart.java
    entity --> SysPackPermission.java
    entity --> SysAnnouncementSend.java
    entity --> SysLog.java
    entity --> SysDepartRole.java
    entity --> SysUserTenant.java
    entity --> SysDepartPermission.java
    entity --> SysCategory.java
    entity --> SysThirdAccount.java
    entity --> SysFormFile.java
    entity --> SysDictItem.java
    entity --> SysUserAgent.java
    entity --> SysFillRule.java
    entity --> SysGatewayRoute.java
    entity --> SysRoleIndex.java
    entity --> SysDataLog.java
    entity --> SysUserDepart.java
    entity --> SysPermissionDataRule.java
    entity --> SysUserRole.java
    entity --> SysDataSource.java
```

该流程图展示了在`entity`文件夹下的多个Java文件，这些文件代表了系统中不同的实体类。每个实体类都与系统的某个功能或模块相关，涵盖了用户、角色、权限、部门等多个方面的数据结构。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [SysRole.java](SysRole.md) | file | SysRole类包含角色ID、名称、编码、描述、创建人、创建时间、更新人、更新时间和租户ID。 |
| [SysTableWhiteList.java](SysTableWhiteList.md) | file | 系统表白名单类含主键、表名、字段名、状态、创建及更新信息。 |
| [SysRolePermission.java](SysRolePermission.md) | file | SysRolePermission类存储角色与权限关联信息，包含ID、角色ID、权限ID等字段。 |
| [SysPermission.java](SysPermission.md) | file | SysPermission类定义系统权限，包含ID、父ID、菜单名等属性。 |
| [SysUserPosition.java](SysUserPosition.md) | file | 用户职位关系表记录用户与职位关联信息，包含主键、用户ID、职位ID及操作日志。 |
| [SysUserRole.java](SysUserRole.md) | file | SysUserRole类含用户ID、角色ID、租户ID，支持链式调用和序列化。 |
| [SysDataLog.java](SysDataLog.md) | file | SysDataLog类记录系统数据日志，含创建、更新及数据内容字段。 |
| [SysUserAgent.java](SysUserAgent.md) | file | SysUserAgent类管理用户代理信息，包括用户名、代理人、时间、状态等字段。 |
| [SysCategory.java](SysCategory.md) | file | SysCategory类表示系统分类，含ID、父节点、名称、编码，支持按编码长度排序。 |
| [SysUserTenant.java](SysUserTenant.md) | file | SysUserTenant类记录用户与租户关系，包含主键、用户ID、租户ID、状态及创建更新信息。 |
| [SysDataSource.java](SysDataSource.md) | file | 多数据源管理类，涵盖ID、编码、名称、数据库类型、驱动类、地址、用户名、密码等字段。 |
| [SysPermissionDataRule.java](SysPermissionDataRule.md) | file | SysPermissionDataRule类包含权限规则ID、菜单ID、规则名称、字段、条件、规则值、状态及创建修改信息。 |
| [SysUserDepart.java](SysUserDepart.md) | file | SysUserDepart类映射用户与部门关系，包含id、用户id和部门id字段。 |
| [SysRoleIndex.java](SysRoleIndex.md) | file | SysRoleIndex类用于角色首页配置，包含ID、编码、路由、组件、菜单、优先级、状态、创建人、创建日期、更新人、更新日期及部门字段。 |
| [SysGatewayRoute.java](SysGatewayRoute.md) | file | SysGatewayRoute类管理网关路由，含主键、路由ID等服务配置，支持前缀忽略、重试等功能。 |
| [SysFillRule.java](SysFillRule.md) | file | SysFillRule类定义填值规则，包含ID、名称、Code、实现类、参数及操作信息。 |
| [SysDictItem.java](SysDictItem.md) | file | SysDictItem类包含字典项ID、字典ID、文本、值、描述、排序、状态、创建更新信息及颜色。 |
| [SysFormFile.java](SysFormFile.md) | file | SysFormFile类存储表单评论文件信息，含ID、表名、数据ID等关键字段。 |
| [SysThirdAccount.java](SysThirdAccount.md) | file | 第三方登录账号表包含编号、登录ID、来源、头像、状态、删除状态、真实姓名、用户UUID、账号、创建人、创建日期、修改人、修改日期、租户ID。 |
| [SysDepartPermission.java](SysDepartPermission.md) | file | 部门权限表类包含id、部门id、权限id和数据规则id字段。 |
| [SysDepartRole.java](SysDepartRole.md) | file | 部门角色类包含ID、部门ID、角色名称、编码、描述及创建更新信息。 |
| [SysLog.java](SysLog.md) | file | SysLog类记录系统日志，包含ID、时间、操作人、请求、日志和操作类型等字段。 |
| [SysAnnouncementSend.java](SysAnnouncementSend.md) | file | 系统公告发送类包含ID、公告ID、用户ID、阅读状态、时间及操作人信息。 |
| [SysPackPermission.java](SysPackPermission.md) | file | SysPackPermission类定义产品包菜单关系，含主键、名称、菜单ID及创建更新信息。 |
| [SysDepart.java](SysDepart.md) | file | SysDepart类管理部门信息，含ID、父部门、名称等字段，支持企业微信和钉钉对接。 |
| [SysAnnouncement.java](SysAnnouncement.md) | file | SysAnnouncement类定义公告，含标题、内容、时间、发布人、优先级、类型、状态等字段。 |
| [SysTenantPack.java](SysTenantPack.md) | file | SysTenantPack类管理租户产品包，包含主键、租户ID、产品包名等字段。 |
| [SysCheckRule.java](SysCheckRule.md) | file | SysCheckRule类定义编码校验规则，包含主键、名称、Code、JSON、描述及时间、人员字段。 |
| [SysDict.java](SysDict.md) | file | SysDict类包含字典ID、类型、名称、编码、描述、删除状态、创建更新信息、租户ID和低代码应用ID。 |
| [SysDepartRoleUser.java](SysDepartRoleUser.md) | file | 部门角色人员信息类包含主键id、用户id和角色id字段。 |
| [SysPosition.java](SysPosition.md) | file | 职务表类含ID、编码、名称、职级、公司ID，支持链式调用。 |
| [SysTenant.java](SysTenant.md) | file | SysTenant类存储租户信息，含ID、名称、创建人、时间、状态、行业、规模、地址等字段。 |
| [SysUser.java](SysUser.md) | file | SysUser类包含用户信息字段，支持序列化和Excel导出。 |
| [SysDepartRolePermission.java](SysDepartRolePermission.md) | file | 部门角色权限类包含ID、部门ID、角色ID、权限ID、数据规则ID、操作时间和操作IP字段。 |
| [SysThirdAppConfig.java](SysThirdAppConfig.md) | file | 第三方配置表包含编号、租户ID、应用标识、应用ID、密钥、企业ID、类别、启用状态及创建修改日期。 |
| [SysComment.java](SysComment.md) | file | 系统评论回复表记录ID、表名、数据ID、用户ID、评论ID、回复内容及创建更新信息。 |
| [SysTenantPackUser.java](SysTenantPackUser.md) | file | 租户产品包用户关系表类，含ID、租户包ID、用户ID、租户ID、创建更新信息及状态字段。 |


