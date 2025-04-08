# 基础信息

|      |      |
|------|------|
| 名称 | controller |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/system/controller |
| 包名 | JeecgBoot.jeecg-boot.jeecg-module-system.jeecg-system-biz.src.main.java.org.jeecg.modules.system.controller |
| 概述说明 | 第三方登录控制器处理微信、钉钉等登录，包括认证、回调、绑定和Token生成。 |

# 说明

## 概述

该代码模块是一个基于JeecgBoot框架的系统管理模块，涵盖了多个核心功能，包括用户管理、权限控制、数据管理、文件处理、日志管理、第三方登录、公告管理、字典管理、部门管理、角色管理、租户管理、编码校验规则管理等。模块通过多个控制器实现了这些功能，提供了全面的系统管理解决方案，支持多租户隔离、数据导入导出、分页查询、批量操作等高级功能，旨在提升系统的灵活性、安全性和管理效率。

## 主要业务场景

1. **用户管理与登录**：
   - 用户登录、验证码校验、用户信息获取、退出登录等功能由`LoginController`处理。
   - 用户管理（查询、添加、编辑、删除、冻结、解冻、修改密码等）由`SysUserController`负责。
   - 在线用户管理和强制退出功能由`SysUserOnlineController`实现。

2. **权限控制**：
   - 菜单、角色和部门权限的增删改查及授权功能由`SysPermissionController`处理。
   - 部门角色管理和数据规则管理由`SysDepartRoleController`负责。
   - 系统角色管理（分页查询、添加、编辑、删除等）由`SysRoleController`实现。

3. **数据管理**：
   - 多数据源管理（分页查询、添加、编辑、删除、导入导出等）由`SysDataSourceController`处理。
   - 字典数据管理（查询、新增、编辑、删除、导入导出等）由`SysDictController`和`SysDictItemController`负责。
   - 分类字典管理（新增、删除、修改、查询、树形结构处理等）由`SysCategoryController`实现。

4. **文件处理**：
   - 文件上传、预览、下载及权限验证由`CommonController`处理。
   - 文件上传路径合法性检查及文件信息保存由`SysUploadController`负责。

5. **日志管理**：
   - 日志查询、删除、批量删除及关键词过滤由`SysLogController`处理。
   - 数据日志查询、对比及版本信息获取由`SysDataLogController`负责。

6. **第三方登录与集成**：
   - 微信、钉钉等第三方平台登录、用户绑定及Token生成由`ThirdLoginController`处理。
   - 企业微信和钉钉的配置、同步及消息测试功能由`ThirdAppController`负责。
   - 企业微信证书验证由`WechatVerifyController`处理。

7. **公告管理**：
   - 公告的增删改查、发布、撤销、同步等功能由`SysAnnouncementController`和`SysAnnouncementSendController`处理。

8. **部门管理**：
   - 部门信息的查询、添加、编辑、删除及树形结构展示由`SysDepartController`负责。
   - 部门权限管理（分页查询、添加、编辑、删除等）由`SysDepartPermissionController`处理。

9. **租户管理**：
   - 租户信息的查询、添加、编辑、删除及默认产品包同步由`SysTenantController`负责。

10. **编码校验规则管理**：
    - 编码校验规则的增删改查、导入导出及规则执行由`SysCheckRuleController`和`SysFillRuleController`处理。

11. **其他功能**：
    - 表单评论文件管理（增删改查、导入导出等）由`SysFormFileController`负责。
    - 角色首页配置管理（分页查询、添加、编辑、删除等）由`SysRoleIndexController`处理。
    - 网关路由管理（更新、查询、删除、还原、复制等）由`SysGatewayRouteController`实现。


### 包内部结构视图

```mermaid
graph TD
    controller --> ThirdLoginController.java
    controller --> SysAnnouncementSendController.java
    controller --> SysDataSourceController.java
    controller --> SysDictController.java
    controller --> SysDepartPermissionController.java
    controller --> SysUploadController.java
    controller --> SysUserOnlineController.java
    controller --> SysFormFileController.java
    controller --> SysCategoryController.java
    controller --> SysLogController.java
    controller --> SysDepartController.java
    controller --> SysTableWhiteListController.java
    controller --> WechatVerifyController.java
    controller --> SysPositionController.java
    controller --> SysCommentController.java
    controller --> CommonController.java
    controller --> SysDepartRoleController.java
    controller --> SysDataLogController.java
    controller --> SysDictItemController.java
    controller --> DuplicateCheckController.java
    controller --> SysGatewayRouteController.java
    controller --> SysRoleController.java
    controller --> SysUserAgentController.java
    controller --> SysTenantController.java
    controller --> SysFillRuleController.java
    controller --> SysCheckRuleController.java
    controller --> SysPermissionController.java
    controller --> SysUserController.java
    controller --> LoginController.java
    controller --> ThirdAppController.java
    controller --> SysAnnouncementController.java
    controller --> SysRoleIndexController.java
```

该流程图展示了一个名为`controller`的文件夹下的多个控制器文件。这些控制器文件涵盖了系统的各种功能模块，如用户管理、角色管理、数据源管理、公告管理等。每个控制器文件都从`controller`节点延伸出来，清晰地展示了它们的层级关系。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [SysPositionController.java](SysPositionController.md) | file | 职务表控制器具备分页查询、增删改、导出导入及多租户隔离功能。 |
| [SysDepartController.java](SysDepartController.md) | file | 部门管理系统支持查询、添加、编辑、删除、导入导出，树形展示和异步加载。 |
| [SysFormFileController.java](SysFormFileController.md) | file | 控制器实现评论文件的增删改查及导入导出功能。 |
| [SysDataSourceController.java](SysDataSourceController.md) | file | 多数据源管理控制器支持增删改查、批量操作及数据导入导出功能。 |
| [ThirdLoginController.java](ThirdLoginController.md) | file | 第三方登录控制器处理微信、钉钉等认证、回调、用户绑定及Token生成。 |
| [ThirdAppController.java](ThirdAppController.md) | file | 第三方应用控制器管理企业微信和钉钉的配置、同步及消息测试。 |
| [SysPermissionController.java](SysPermissionController.md) | file | 系统权限管理控制器实现菜单、角色、部门权限的增删改查及授权功能。 |
| [SysTenantController.java](SysTenantController.md) | file | 控制器负责租户管理的查询、添加、编辑、删除及同步默认产品包操作。 |
| [DuplicateCheckController.java](DuplicateCheckController.md) | file | 控制器校验数据：空值返回，非空检查可用性后返回结果。 |
| [SysDepartRoleController.java](SysDepartRoleController.md) | file | 部门角色管理控制器具备增删改查、角色分配、数据规则管理及Excel导入导出功能。 |
| [SysRoleIndexController.java](SysRoleIndexController.md) | file | 角色首页配置控制器提供分页查询、增删改、导入导出功能。 |
| [SysAnnouncementController.java](SysAnnouncementController.md) | file | 系统公告控制器支持增删改查、发布、撤销、同步，具备多租户、XSS防护及第三方消息推送功能。 |
| [LoginController.java](LoginController.md) | file | LoginController负责用户登录、验证码校验、信息获取和退出登录。 |
| [SysUserController.java](SysUserController.md) | file | SysUserController管理用户操作，支持多租户隔离和部门管理。 |
| [SysCheckRuleController.java](SysCheckRuleController.md) | file | 编码校验规则控制器具备分页查询、增删改查、批量操作及数据导入导出功能。 |
| [SysFillRuleController.java](SysFillRuleController.md) | file | 控制器管理填值规则的查询、增删改、导入导出及执行操作。 |
| [SysUserAgentController.java](SysUserAgentController.md) | file | SysUserAgentController提供用户代理人管理功能，支持查询、增删改、导入导出操作。 |
| [SysRoleController.java](SysRoleController.md) | file | 系统角色管理控制器支持分页查询、增删改及租户隔离与权限控制。 |
| [SysGatewayRouteController.java](SysGatewayRouteController.md) | file | 网关路由管理控制器支持更新、查询、删除、还原和复制路由操作。 |
| [SysDictItemController.java](SysDictItemController.md) | file | SysDictItemController实现字典数据的增删改查及重复校验。 |
| [SysDataLogController.java](SysDataLogController.md) | file | SysDataLogController支持日志查询、对比和版本信息获取。 |
| [CommonController.java](CommonController.md) | file | CommonController处理文件操作，支持多种存储，含安全检查与路径处理。 |
| [SysCommentController.java](SysCommentController.md) | file | 系统评论回复控制器支持查询、添加、删除、编辑及文件管理。 |
| [WechatVerifyController.java](WechatVerifyController.md) | file | 企业微信证书验证控制器处理验证请求并返回代码。 |
| [SysTableWhiteListController.java](SysTableWhiteListController.md) | file | 系统表白名单控制器支持分页、增删改查及批量操作。 |
| [SysLogController.java](SysLogController.md) | file | SysLogController支持日志查询、删除、批量删除，分页和关键词过滤。 |
| [SysCategoryController.java](SysCategoryController.md) | file | SysCategoryController负责分类字典的增删改查、分页查询、导出导入及树结构加载操作。 |
| [SysUserOnlineController.java](SysUserOnlineController.md) | file | SysUserOnlineController管理在线用户及强制退出，依赖Redis处理令牌和缓存。 |
| [SysUploadController.java](SysUploadController.md) | file | SysUploadController处理文件上传，验证路径，保存信息并返回结果。 |
| [SysDepartPermissionController.java](SysDepartPermissionController.md) | file | 部门权限控制器支持分页查询、增删改、批量删除及数据规则管理。 |
| [SysDictController.java](SysDictController.md) | file | 系统字典控制器支持查询、增删改、导入导出及缓存刷新功能。 |
| [SysAnnouncementSendController.java](SysAnnouncementSendController.md) | file | 控制器实现公告的增删改查、批量操作、状态更新及消息获取功能。 |


