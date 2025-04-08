# 基础信息

|      |      |
|------|------|
| 名称 | org |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-boot-base-core/src/main/java/org |
| 包名 | JeecgBoot.jeecg-boot.jeecg-boot-base-core.src.main.java.org |
| 概述说明 | JeecgBoot核心模块提供工具类、安全过滤、数据加密、动态数据库管理等功能，适用于复杂业务场景。 |

# 说明

## 概述

该代码模块是JeecgBoot项目的核心部分，主要包含`jeecg-boot-base-core`模块，提供了丰富的工具类、功能组件和业务处理逻辑，涵盖了字符串和文件的安全过滤、日期时间处理、数据加密、SQL解析、动态数据库管理、文件操作、短信发送、反射操作、浏览器检测、日志管理、Token管理、应用上下文管理、常量管理、Elasticsearch集成、数据传输与业务处理、异常处理、敏感数据处理、切面编程等多个方面。模块通过多种机制确保系统的安全性、灵活性和高效性，适用于复杂的业务场景和多样化的开发需求。

## 主要业务场景

1. **字符串和文件安全过滤**：
   - **字符串安全过滤**：通过`StrAttackFilter`类过滤字符串中的特殊字符，防止字符串注入攻击，适用于表单提交、API请求等场景。
   - **文件类型安全过滤**：通过`SsrfFileTypeFilter`类确保上传或下载的文件类型安全，防止恶意文件上传，适用于文件上传和下载操作。

2. **日期时间处理**：
   - **日期时间格式化与计算**：`DateUtils`类提供日期时间的格式化、转换、计算和比较功能，适用于处理日期时间相关需求。
   - **日期范围获取**：`DateRangeUtils`类通过枚举获取多种日期范围，简化了日期范围获取的过程，适用于处理不同时间段的场景。

3. **数据加密与安全**：
   - **AES加密与解密**：`AesEncryptUtil`类简化了AES加密的配置和使用，适用于数据传输和存储的加密保护。
   - **SQL注入检测与防范**：`SqlInjectionUtil`类通过关键词过滤、正则匹配和注释校验，防止SQL注入攻击，适用于数据库操作场景。

4. **SQL解析与管理**：
   - **SQL查询解析与表信息提取**：`JSqlParserAllTableManager`类解析SQL语句，提取表信息，适用于多表查询和嵌套查询场景。
   - **SQL模板解析**：`FreemarkerParseFactory`类解析SQL模板，支持动态生成SQL语句，适用于需要动态生成SQL的场景。

5. **动态数据库管理**：
   - **数据库类型识别与方言映射**：`DbTypeUtils`类识别数据库类型并返回相应的方言信息，适用于多种数据库的兼容性操作。
   - **动态数据源管理**：`DynamicDBUtil`类支持动态数据源的切换和资源优化，适用于频繁切换数据源的场景。

6. **文件操作与管理**：
   - **MinIO文件管理**：`MinioUtil`类支持文件的上传、下载和删除操作，适用于MinIO文件存储管理。
   - **文件下载**：`FileDownloadUtils`类支持多种下载方式，适用于单文件下载、多文件压缩下载和网络资源下载。

7. **短信发送与限制**：
   - **短信发送**：`DySmsHelper`类提供短信发送功能，适用于需要发送短信的场景。
   - **短信发送限制**：`DySmsLimit`类限制单一IP地址的短信发送频率，防止短信滥发，适用于短信发送频率控制。

8. **反射操作与工具类**：
   - **反射操作**：`ReflectHelper`类用于获取和设置对象的属性值，处理Map类型数据，适用于反射机制的核心应用场景。
   - **多功能工具类**：`CommonUtils`类集成了文件上传、文件名处理、中文检测、数据库类型获取和URL生成等功能，适用于多种常见操作。

9. **浏览器检测与日志管理**：
   - **浏览器检测**：`BrowserUtils`类检测浏览器类型、版本、语言及设备类型，适用于兼容性优化和用户行为分析。
   - **日志管理**：`PmsUtil`类用于错误日志的保存和生成，适用于系统运行中的问题追踪和分析。

10. **Token管理与应用上下文**：
    - **Token管理**：`TokenUtils`类提取和验证token，支持token刷新和用户信息获取，适用于用户认证和授权场景。
    - **应用上下文管理**：`SpringContextUtils`类获取应用中的Bean实例和处理HTTP请求，适用于与Spring框架的交互。

11. **数据安全与隐私保护**：
    - **SQL黑名单校验**：`AbstractQueryBlackListHandler`类拦截敏感SQL查询，防止未经授权的数据访问，适用于数据访问权限控制。
    - **数据加密与签名**：`SecurityTools`类提供AES加密、RSA签名和密钥生成功能，适用于数据的安全传输和存储。

12. **常量管理**：
    - **符号常量管理**：通过`SymbolConstant`类定义和使用常见的符号常量，减少代码中的硬编码，提高代码的可读性和一致性。
    - **数据库常量管理**：`DataBaseConstant`类用于定义与数据库相关的常量，如表名、字段名等，便于在数据库操作时进行统一管理。
    - **角色首页配置管理**：`DynamicTableConstant`类用于定义角色首页配置表名，兼容Vue2和Vue3框架，确保在不同版本的Vue框架下都能正常使用。
    - **省市区数据管理**：`ProvinceCityArea`类用于处理省市区数据，提供获取文本和编码的功能，支持精准匹配和初始化数据，确保数据的完整性和准确性。
    - **消息类型管理**：`VxeSocketConst`类定义了消息类型和数据常量，主要用于心跳检测、通用数据传递以及更新vxe table数据，确保系统通信的稳定性和数据的一致性。
    - **WebSocket通信管理**：`WebsocketConst`类用于定义WebSocket通信中的消息JSON键和类型常量，确保消息格式的一致性和可维护性。
    - **公文发文管理**：`FillRuleConstant`类用于定义公文发文、部门和分类字典编码的常量，确保在处理公文发文、部门管理和分类编码时的一致性和准确性。
    - **枚举常量管理**：`enums`目录下的枚举类文件用于定义系统中各种常量类型，如模块类型、消息类型、文件类型、操作类型等，为系统提供了统一的常量定义，使得代码更加规范化和易于维护。

13. **Elasticsearch集成与操作**：
    - **复杂查询条件构建**：`QueryStringBuilder`类用于灵活构建复杂的查询条件，支持AND、OR、NOT三种逻辑操作，适用于需要动态生成查询字符串的场景。
    - **Elasticsearch数据管理**：`JeecgElasticsearchTemplate`类封装了与Elasticsearch交互的核心功能，包括索引的增删查改、数据的保存、更新以及查询操作，适用于Elasticsearch数据管理场景。

14. **数据传输与业务处理**：
    - **文件上传与下载**：`FileUploadDTO`和`FileDownDTO`类分别用于处理文件上传和下载操作，确保文件操作功能的顺利实现。
    - **消息传输与模板管理**：`MessageDTO`、`BusMessageDTO`、`TemplateDTO`、`TemplateMessageDTO`和`BusTemplateMessageDTO`类用于封装和传递消息及模板信息，确保消息传输和模板管理的统一性和一致性。
    - **数据日志记录**：`DataLogDTO`类用于记录数据日志，支持不同场景下的实例化需求。
    - **在线认证**：`OnlineAuthDTO`类用于在线认证，确保数据在网络传输或存储时的完整性和一致性。
    - **日志管理**：`LogDTO`类用于记录日志信息，便于后续的日志分析和问题排查。
    - **接口返回信息封装**：`Result`类用于封装接口返回的信息，提供操作是否成功、描述性信息、状态码、返回数据和时间戳等全面反馈。

15. **异常处理**：
    - **断言异常处理**：`JeecgBootAssertException`处理断言相关的异常，提供详细的错误信息和错误码，便于开发者快速定位和解决问题。
    - **401异常处理**：`JeecgBoot401Exception`专门用于处理401未授权异常，增强代码的健壮性。
    - **业务逻辑错误提示**：`JeecgBootBizTipException`用于处理业务逻辑中的错误提示，便于系统记录和排查问题。
    - **SQL注入异常处理**：`JeecgSqlInjectionException`专门用于捕获和抛出SQL注入相关的异常，增强代码的安全性。
    - **通用异常处理**：`JeecgBootException`作为基础异常类，用于处理框架中的通用异常情况。
    - **异常处理器**：`JeecgBootExceptionHandler`负责自动检测和处理各类异常，记录详细的日志信息，并向用户或调用方返回相应的错误信息，确保系统在遇到异常时能够提供明确的反馈和指导。

16. **敏感数据处理**：
    - **数据脱敏**：通过`Sensitive`和`SensitiveField`注解对数据进行脱敏处理，确保敏感信息不会直接暴露。
    - **数据加密与解密**：`SensitiveInfoUtil`和`SensitiveDataAspect`对敏感数据进行加密和解密操作，确保数据在存储和传输过程中的安全性。
    - **数据编码与解码**：`SensitiveEncode`和`SensitiveDecode`注解对敏感数据进行编码和解码，保护数据的隐私并恢复原始数据。
    - **JSON序列化中的敏感数据处理**：`SensitiveSerialize`类在JSON序列化过程中自动识别并保护敏感数据，防止数据泄露。
    - **灵活配置与自动化处理**：通过注解和切面，开发者可以灵活配置哪些字段需要脱敏、加密、解密、编码或解码，同时实现自动化处理，提高代码的可维护性和安全性。

17. **切面编程**：
    - **自动化日志记录**：`AutoLogAspect`类自动记录方法的执行时间、请求参数以及用户信息等关键数据，便于后续的日志分析和问题排查。
    - **权限控制**：`PermissionDataAspect`类负责处理请求路径，通过查询数据权限来验证用户是否有权访问特定资源，确保系统的安全性。
    - **数据字典处理**：`DictAspect`类实现了字典数据的自动注入，支持单字典和表字典的自动翻译功能，并集成了Redis缓存机制，提升系统的响应速度和效率。
    - **动态表处理**：`DynamicTable`注解允许在运行时动态切换或处理数据库表，适用于多租户或动态数据源场景。
    - **在线认证**：`OnlineAuth`注解用于实现用户的在线认证功能，确保用户在访问系统资源时处于登录状态。

通过这些功能，该模块能够满足复杂业务场景下对安全性、灵活性和高效性的多样化需求，提升系统的整体性能和可维护性。


### 包内部结构视图

```mermaid
graph TD
    org --> jeecg
    jeecg --> common
    common --> util
    util --> filter
    filter --> StrAttackFilter.java
    filter --> SsrfFileTypeFilter.java
    util --> oConvertUtils.java
    util --> FillRuleUtil.java
    util --> IpUtils.java
    util --> superSearch
    superSearch --> QueryRuleVo.java
    superSearch --> ObjectParseUtil.java
    superSearch --> QueryRuleEnum.java
    util --> RestDesformUtil.java
    util --> DateUtils.java
    util --> DateRangeUtils.java
    util --> Md5Util.java
    util --> AssertUtils.java
    util --> encryption
    encryption --> AesEncryptUtil.java
    encryption --> EncryptedString.java
    util --> RestUtil.java
    util --> sqlparse
    sqlparse --> vo
    vo --> SelectSqlInfo.java
    sqlparse --> JSqlParserAllTableManager.java
    sqlparse --> JSqlParserUtils.java
    util --> MinioUtil.java
    util --> SqlInjectionUtil.java
    util --> dynamic
    dynamic --> db
    db --> DbTypeUtils.java
    db --> FreemarkerParseFactory.java
    db --> DynamicDBUtil.java
    db --> DataSourceCachePool.java
    util --> PasswordUtil.java
    util --> HTMLUtils.java
    util --> CommonUtils.java
    util --> sqlInjection
    sqlInjection --> InjectionSyntaxObjectAnalyzer.java
    sqlInjection --> parse
    parse --> ParserSupport.java
    parse --> ConstAnalyzer.java
    parse --> SqlSyntaxNormalizer.java
    sqlInjection --> InjectionAstNodeVisitor.java
    sqlInjection --> SqlInjectionAnalyzer.java
    util --> oss
    oss --> OssBootUtil.java
    util --> YouBianCodeUtil.java
    util --> MyClassLoader.java
    util --> UUIDGenerator.java
    util --> ImportExcelUtil.java
    util --> DySmsLimit.java
    util --> DySmsHelper.java
    util --> FileDownloadUtils.java
    util --> ReflectHelper.java
    util --> BrowserUtils.java
    util --> PmsUtil.java
    util --> TokenUtils.java
    util --> SpringContextUtils.java
    util --> security
    security --> AbstractQueryBlackListHandler.java
    security --> entity
    entity --> SecurityReq.java
    entity --> SecuritySignReq.java
    entity --> SecuritySignResp.java
    entity --> MyKeyPair.java
    entity --> SecurityResp.java
    security --> SecurityTools.java
    security --> JdbcSecurityUtil.java
    util --> BrowserType.java
    common --> constant
    constant --> TenantConstant.java
    constant --> DataBaseConstant.java
    constant --> SymbolConstant.java
    constant --> DynamicTableConstant.java
    constant --> enums
    enums --> ModuleType.java
    enums --> Vue3MessageHrefEnum.java
    enums --> SysAnnmentTypeEnum.java
    enums --> CgformEnum.java
    enums --> ClientTerminalTypeEnum.java
    enums --> DySmsEnum.java
    enums --> DateRangeEnum.java
    enums --> FileTypeEnum.java
    enums --> EmailTemplateEnum.java
    enums --> MessageTypeEnum.java
    enums --> RoleIndexConfigEnum.java
    enums --> OperateTypeEnum.java
    constant --> ProvinceCityArea.java
    constant --> VxeSocketConst.java
    constant --> CommonConstant.java
    constant --> ServiceNameConstants.java
    constant --> FillRuleConstant.java
    constant --> WebsocketConst.java
    constant --> CommonSendStatus.java
    common --> es
    es --> QueryStringBuilder.java
    es --> JeecgElasticsearchTemplate.java
    common --> handler
    handler --> IFillRuleHandler.java
    common --> api
    api --> dto
    dto --> FileUploadDTO.java
    dto --> message
    message --> BusMessageDTO.java
    message --> MessageDTO.java
    message --> TemplateDTO.java
    message --> BusTemplateMessageDTO.java
    message --> TemplateMessageDTO.java
    dto --> DataLogDTO.java
    dto --> OnlineAuthDTO.java
    dto --> FileDownDTO.java
    dto --> LogDTO.java
    api --> CommonAPI.java
    api --> vo
    vo --> Result.java
    common --> system
    system --> util
    util --> JeecgDataAutorUtils.java
    util --> ResourceUtil.java
    util --> SqlConcatUtil.java
    util --> JwtUtil.java
    system --> vo
    vo --> SysPermissionDataRuleModel.java
    vo --> DictQuery.java
    vo --> SysCategoryModel.java
    vo --> ComboModel.java
    vo --> SelectTreeModel.java
    vo --> SysUserCacheInfo.java
    vo --> DictModelMany.java
    vo --> DictModel.java
    vo --> SysDepartModel.java
    vo --> UserAccountInfo.java
    vo --> LoginUser.java
    vo --> SysFilesModel.java
    vo --> DynamicDataSourceModel.java
    system --> annotation
    annotation --> EnumDict.java
    system --> enhance
    enhance --> UserFilterEnhance.java
    system --> base
    base --> entity
    entity --> JeecgEntity.java
    base --> controller
    controller --> JeecgController.java
    base --> service
    service --> JeecgService.java
    service --> impl
    impl --> JeecgServiceImpl.java
    system --> query
    query --> QueryGenerator.java
    query --> QueryRuleEnum.java
    query --> MatchTypeEnum.java
    query --> QueryCondition.java
    common --> exception
    exception --> JeecgBootAssertException.java
    exception --> JeecgBoot401Exception.java
    exception --> JeecgBootExceptionHandler.java
    exception --> JeecgBootBizTipException.java
    exception --> JeecgSqlInjectionException.java
    exception --> JeecgBootException.java
    common --> desensitization
    desensitization --> util
    util --> SensitiveInfoUtil.java
    desensitization --> SensitiveSerialize.java
    desensitization --> enums
    enums --> SensitiveEnum.java
    desensitization --> annotation
    annotation --> Sensitive.java
    annotation --> SensitiveDecode.java
    annotation --> SensitiveEncode.java
    annotation --> SensitiveField.java
    desensitization --> aspect
    aspect --> SensitiveDataAspect.java
    common --> aspect
    aspect --> AutoLogAspect.java
    aspect --> annotation
    annotation --> AutoLog.java
    annotation --> PermissionData.java
    annotation --> Dict.java
    annotation --> DynamicTable.java
    annotation --> AutoDict.java
    annotation --> OnlineAuth.java
    aspect --> DictAspect.java
    aspect --> UrlMatchEnum.java
    aspect --> PermissionDataAspect.java
    jeecg --> modules
    modules --> base
    base --> service
    service --> BaseCommonService.java
    service --> impl
    impl --> BaseCommonServiceImpl.java
    base --> mapper
    mapper --> BaseCommonMapper.java
    mapper --> xml
    jeecg --> config
    config --> filter
    filter --> RequestBodyReserveFilter.java
    filter --> WebsocketFilter.java
    config --> AutoPoiConfig.java
    config --> sign
    sign --> util
    util --> SignUtil.java
    util --> HttpUtils.java
    util --> BodyReaderHttpServletRequestWrapper.java
    sign --> interceptor
    interceptor --> SignAuthConfiguration.java
    interceptor --> SignAuthInterceptor.java
    config --> JeecgSmsTemplateConfig.java
    config --> shiro
    shiro --> ignore
    ignore --> IgnoreAuthPostProcessor.java
    ignore --> InMemoryIgnoreAuth.java
    shiro --> IgnoreAuth.java
    shiro --> filters
    filters --> CustomShiroFilterFactoryBean.java
    filters --> ResourceCheckFilter.java
    filters --> JwtFilter.java
    shiro --> ShiroRealm.java
    shiro --> JwtToken.java
    shiro --> ShiroConfig.java
    config --> StaticConfig.java
    config --> AutoPoiDictConfig.java
    config --> RestTemplateConfig.java
    config --> vo
    vo --> Elasticsearch.java
    vo --> Path.java
    vo --> WeiXinPay.java
    vo --> DomainUrl.java
    vo --> Shiro.java
    vo --> Firewall.java
    vo --> BaiduApi.java
    config --> firewall
    firewall --> interceptor
    interceptor --> LowCodeModeConfiguration.java
    interceptor --> enums
    enums --> LowCodeUrlsEnum.java
    interceptor --> LowCodeModeInterceptor.java
    firewall --> SqlInjection
    SqlInjection --> IDictTableWhiteListHandler.java
    SqlInjection --> SysDictTableWhite.java
    config --> DruidWallConfigRegister.java
    config --> oss
    oss --> OssConfiguration.java
    oss --> MinioConfig.java
    config --> mybatis
    mybatis --> MybatisInterceptor.java
    mybatis --> interceptor
    interceptor --> DynamicDatasourceInterceptor.java
    mybatis --> TenantContext.java
    mybatis --> MybatisPlusSaasConfig.java
    mybatis --> ThreadLocalDataHelper.java
    mybatis --> JeecgTenantParser.java
    mybatis --> aspect
    aspect --> DynamicTableAspect.java
    config --> WebMvcConfiguration.java
    config --> DruidConfig.java
    config --> Swagger3Config.java
    config --> CorsFilterCondition.java
    config --> JeecgBaseConfig.java
    config --> Swagger2Config.java
    config --> WebSocketConfig.java
    config --> JeecgCloudCondition.java
```

该流程图展示了JeecgBoot项目中核心模块的目录结构及其层级关系。从根目录`org`开始，逐步展开到`jeecg`、`common`、`util`、`filter`等子目录，最终展示出各个Java文件的层级关系。该图清晰地反映了项目中各个模块的依赖关系和文件组织结构，便于开发者快速理解和定位相关代码。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [jeecg](jeecg/_module.md) | package | JeecgBoot核心模块提供工具类、安全过滤、数据加密、动态数据库管理等功能，适用于复杂业务场景。 |


