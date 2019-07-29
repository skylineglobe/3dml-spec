# 3DML开源说明

version 1.0.1

# 概述

3DML 格式是针对传输和浏览大量 3D 空间数据设计的，包括地形表面、3D 城市模型和BIM/CAD。3DML 基于开源的 SQLite 数据库和扩展组件 SpatialLite，它定义了包括分层分级的模型数据、矢量信息和工程信息的数据库结构。

3DML 数据库所包括的相关的块数据格式以及相关的矢量信息都是开源的，都不依赖其他特殊厂商的解决方案、技术或者产品。

3DML 数据库可以用于本地 3D 模型资源或者在线的网络服务。

# 3DML 的主要作用
3DML 主要用于：
* 地形网格模型
* 城市网格模型
* 单个模型
* BIM 和 CAD 模型

![image](https://github.com/skylineglobe/3dml-spec/blob/master/images/yongyu.jpg)

# 3DML 文件格式

3DML 文件包含网格数据、矢量图层和元数据。不同分辨率的瓦片数据是按照树状结构进行组织，树上的每个节点都包含更多的子节点。每个节点和其父节点表示相同的信息，但是子节点的分辨率更高。

3DML 文件包含以下表格：

* Version 表-保存 3DML 版本信息。
* Projects 表-保存 3DML 数据集相关信息，包括：
    *  bounding box
    *  唯一 GUID
    *  WKT 格式的数据集坐标系统
