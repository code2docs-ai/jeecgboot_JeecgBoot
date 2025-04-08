# 基础信息

|      |      |
|------|------|
| 名称 | mock |
| 编码语言 | .java |
| 代码路径 | JeecgBoot/jeecg-boot/jeecg-module-demo/src/main/java/org/jeecg/modules/demo/mock |
| 包名 | JeecgBoot.jeecg-boot.jeecg-module-demo.src.main.java.org.jeecg.modules.demo.mock |
| 概述说明 | 代码模块包含MockEntity、VxeMockController和VxeSocket，支持层级关系管理、实时数据模拟和多页面通信。 |

# 说明

## 概述

该代码模块主要围绕模拟数据管理和实时通信功能展开，包含三个核心组件：`MockEntity`、`VxeMockController` 和 `VxeSocket`。`MockEntity` 是一个简单的实体类，用于表示具有层级关系和状态信息的实体。`VxeMockController` 是一个模拟数据操作工具，支持状态管理、拖轮控制和进度条显示等功能，并通过 Socket 实现数据的实时更新。`VxeSocket` 则负责管理 WebSocket 连接，支持多页面通信和事件处理。该模块适用于需要实时数据交互、模拟操作和多页面通信的业务场景。

此外，`MockController` 提供了多个接口，用于读取不同种类的 JSON 文件数据，涵盖了用户信息、角色信息、权限信息、省市县数据、报表数据、磁盘信息以及工作台数据等。通过这些接口，用户可以方便地获取和处理各类结构化数据，满足多种应用场景的需求。

## 主要业务场景

1. **层级关系与状态管理**  
   - 使用 `MockEntity` 类表示具有层级关系（通过 `parentId` 字段）和状态信息（通过 `status` 字段）的实体，适用于需要管理复杂实体关系的场景。

2. **实时数据模拟与操作**  
   - 通过 `VxeMockController` 实现模拟数据的更改和查询，支持状态管理、拖轮控制和进度条显示等功能，适用于需要实时数据交互和模拟操作的场景。

3. **多页面通信与事件处理**  
   - 使用 `VxeSocket` 类管理 WebSocket 连接，支持多页面之间的消息传递和事件处理，适用于需要高效通信和事件管理的多页面应用场景。

4. **结构化数据获取与处理**  
   - 通过 `MockController` 提供的接口，用户可以方便地获取和处理各类结构化数据，如用户信息、角色信息、权限信息、省市县数据、报表数据、磁盘信息以及工作台数据等，适用于需要处理多种类型数据的应用场景。

该模块通过结合实体管理、数据模拟和实时通信功能，提升了数据处理的效率和准确性，适用于需要复杂实体关系、实时数据交互和多页面通信的业务需求。


### 包内部结构视图

```mermaid
graph TD
    mock --> vxe
    mock --> json
    mock --> MockController.java
    vxe --> json
    vxe --> entity
    vxe --> controller
    vxe --> websocket
    entity --> MockEntity.java
    controller --> VxeMockController.java
    websocket --> VxeSocket.java
```

该流程图展示了JeecgBoot项目中`mock`模块的目录结构及其层级关系。`mock`作为根目录，包含`vxe`、`json`和`MockController.java`等子节点。`vxe`目录下进一步细分为`json`、`entity`、`controller`和`websocket`等子目录，每个子目录中包含相应的文件，如`MockEntity.java`、`VxeMockController.java`和`VxeSocket.java`。整个结构清晰地反映了模块的组织方式。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [MockController.java](MockController.md) | file | MockController提供多个接口读取JSON文件，涵盖用户、角色、权限等数据。 |
| [json](json/_module.md) | package | None |
| [vxe](vxe/_module.md) | package | MockEntity类含id、parentId、status字段；VxeMockController支持实时数据更新；VxeSocket管理WebSocket通信。 |


