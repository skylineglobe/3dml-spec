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
    *  BBox
    *  唯一 GUID
    *  WKT 格式的数据集坐标系统
* Index 表-以子树形式存储网格模型的索引信息。
*  mesh 表-包括网格模型的节点块数据，包括几何、贴图和地表。
*  Feature 表-存储用于分类的面状图层的空间表（不在本文档中详细描述）。
关于表格及表格内容更详细的信息请查看表格章节。

3DML 文件结构图:

![image](https://github.com/skylineglobe/3dml-spec/blob/master/images/geshizucheng2.jpg)

子树以二进制数据形式保存了网格图层分层结构。每个子树记录保存了包括BBox、数据块的像素大小、参考和相对子节点的参考等信息。

子树的结构图：

![image](https://github.com/skylineglobe/3dml-spec/blob/master/images/zishu.jpg)

嵌套式子树的结构图：

![image](https://github.com/skylineglobe/3dml-spec/blob/master/images/qiantaozishu.jpg)

# 3DML 优势

## 可分类

3DML 格式存储了网格分类信息，将网格转换成了空间数据。可分类的 3DML 支持读取属性信息和一系列矢量图层操作，包括：

* 空间查询和属性查询
* 快速读取数据
* 可以使用属性数据进行网格分类渲染和作为提示信息
* 根据属性值进行筛选显示对应的网格数据
* 根据空间查询或属性查询的结果创建新的图层

![image](https://github.com/skylineglobe/3dml-spec/blob/master/images/kefenlei.jpg)

## 地面层

3DML 文件格式可以单独读取网格图层的地面信息。这使得网格图层可以替换 3DML 范围内的影像和高程，这样让类似道路线等贴地表的对象可以直接贴在 3DML 地面层上，可能有一点随机的网格地面误差。

![image](https://github.com/skylineglobe/3dml-spec/blob/master/images/dimianceng.jpg)

## 压缩存储优化

3DML 格式是基于 SQLite 数据库和它的 SpatialLite 扩展，用于存储海量的三维空间数据集，可以用在移动端、网页端和桌面端。3DML 是一个单独的二进制文件，存储了所有关于3DML 数据集的信息，包括BBox、坐标系、网格模型块以及用于分类的面图层，这样的存储形式非常方便存储和管理。

## 数据流优化

网格数据存储在多级文件数据库中，这样在加载的时候可以先加载低精度级别的数据，当用户放大浏览到高精度的区域的时候再动态加载高精度的数据。从文件中读取数据时不需要一定是连续的数据，可以是不连续的数据。
