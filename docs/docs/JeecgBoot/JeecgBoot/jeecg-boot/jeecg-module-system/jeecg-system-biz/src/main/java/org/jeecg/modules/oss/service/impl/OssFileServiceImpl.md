# 基础信息

|      |      |
|------|------|
| 名称 | OssFileServiceImpl |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-system/jeecg-system-biz/src/main/java/org/jeecg/modules/oss/service/impl/OssFileServiceImpl.java |
| 包名 | org.jeecg.modules.oss.service.impl |
| 依赖项 | ['com.baomidou.mybatisplus.extension.service.impl.ServiceImpl', 'org.jeecg.common.exception.JeecgBootException', 'org.jeecg.common.util.CommonUtils', 'org.jeecg.common.util.oConvertUtils', 'org.jeecg.common.util.oss.OssBootUtil', 'org.jeecg.modules.oss.entity.OssFile', 'org.jeecg.modules.oss.mapper.OssFileMapper', 'org.jeecg.modules.oss.service.IOssFileService', 'org.springframework.stereotype.Service', 'org.springframework.web.multipart.MultipartFile', 'java.io.IOException'] |
| 概述说明 | OssFileServiceImpl类实现文件上传删除，支持阿里云域名处理。 |

# 说明

OssFileServiceImpl类主要负责实现文件的上传与删除功能，特别支持阿里云原生域名的URL处理。该服务类通过集成阿里云OSS（对象存储服务）的API，提供了高效的文件管理能力。上传功能允许用户将文件存储到阿里云OSS中，并生成对应的访问URL；删除功能则用于从OSS中移除指定文件。此外，该类还支持对阿里云原生域名的处理，确保生成的URL符合阿里云的规范，便于用户直接访问存储的文件。整体设计旨在简化文件操作的复杂性，提升系统的稳定性和可扩展性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| OssFileServiceImpl | class | OssFileServiceImpl类实现文件上传与删除功能，支持阿里云原生域名URL处理。 |



## 类 OssFileServiceImpl

|      |      |
|------|------|
| 访问范围 | @Service("ossFileService");public |
| 类型 | class |
| 名称 | OssFileServiceImpl |
| 说明 | OssFileServiceImpl类实现文件上传与删除功能，支持阿里云原生域名URL处理。 |


### UML类图

```mermaid
classDiagram
    class OssFileServiceImpl {
        +void upload(MultipartFile multipartFile) throws Exception
        +boolean delete(OssFile ossFile)
    }

    class OssFile {
        +String fileName
        +String url
        +void setFileName(String fileName)
        +void setUrl(String url)
        +String getUrl()
        +String getId()
    }

    class MultipartFile {
        +String getOriginalFilename()
    }

    class CommonUtils {
        +String getFileName(String fileName)
    }

    class OssBootUtil {
        +String upload(MultipartFile multipartFile, String path)
        +String getOriginalUrl(String url)
        +void deleteUrl(String url)
    }

    class oConvertUtils {
        +boolean isEmpty(Object obj)
    }

    class JeecgBootException {
        +JeecgBootException(String message)
    }

    class ServiceImpl~T~ {
        +void save(T entity)
        +void removeById(Object id)
    }

    class IOssFileService {
        <<Interface>>
        +void upload(MultipartFile multipartFile) throws Exception
        +boolean delete(OssFile ossFile)
    }

    OssFileServiceImpl --> IOssFileService : 实现
    OssFileServiceImpl --> ServiceImpl~OssFile~ : 继承
    OssFileServiceImpl --> MultipartFile : 依赖
    OssFileServiceImpl --> CommonUtils : 依赖
    OssFileServiceImpl --> OssBootUtil : 依赖
    OssFileServiceImpl --> oConvertUtils : 依赖
    OssFileServiceImpl --> JeecgBootException : 依赖
    OssFileServiceImpl --> OssFile : 依赖
```

**描述：**  
`OssFileServiceImpl` 类实现了 `IOssFileService` 接口，并继承了 `ServiceImpl<OssFile>` 类。该类主要负责文件的上传和删除操作。在 `upload` 方法中，它通过 `MultipartFile` 获取文件名，使用 `CommonUtils` 和 `OssBootUtil` 进行文件处理和上传，并处理异常情况。`delete` 方法则通过 `OssBootUtil` 删除文件，并处理可能的异常。该类依赖多个工具类和异常类来完成其功能。


### 内部方法调用关系图

```mermaid
graph TD
    A["类OssFileServiceImpl"]
    B["方法: upload(MultipartFile multipartFile)"]
    C["方法: delete(OssFile ossFile)"]
    D["获取文件名: multipartFile.getOriginalFilename()"]
    E["处理文件名: CommonUtils.getFileName(fileName)"]
    F["创建OssFile对象: new OssFile()"]
    G["设置文件名: ossFile.setFileName(fileName)"]
    H["上传文件: OssBootUtil.upload(multipartFile, 'upload/test')"]
    I["检查URL是否为空: oConvertUtils.isEmpty(url)"]
    J["抛出异常: throw new JeecgBootException('上传文件失败! ')"]
    K["设置URL: ossFile.setUrl(OssBootUtil.getOriginalUrl(url))"]
    L["保存OssFile对象: this.save(ossFile)"]
    M["删除OssFile对象: this.removeById(ossFile.getId())"]
    N["删除URL: OssBootUtil.deleteUrl(ossFile.getUrl())"]
    O["捕获异常: log.error(ex.getMessage(),ex)"]
    P["返回false"]
    Q["返回true"]

    A --> B
    A --> C
    B --> D
    D --> E
    E --> F
    F --> G
    G --> H
    H --> I
    I -->|是| J
    I -->|否| K
    K --> L
    C --> M
    M --> N
    N --> Q
    N -.-> O
    O --> P
```

这段代码展示了一个名为`OssFileServiceImpl`的类，它实现了文件上传和删除的功能。`upload`方法首先获取并处理文件名，然后创建一个`OssFile`对象并设置文件名，接着上传文件并检查URL是否为空，如果为空则抛出异常，否则设置URL并保存对象。`delete`方法尝试删除`OssFile`对象及其对应的URL，如果操作成功则返回`true`，否则捕获异常并返回`false`。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| delete | boolean | 删除OSS文件，成功返回true，失败返回false并记录错误。 |
| upload | void | 上传文件至阿里云OSS，返回原生域名URL，失败则抛出异常。 |




