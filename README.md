# Quantify-Business-Model

# 1. 项目简介

本项目利用 NLP 技术，致力于从中国上市公司年报中逐步挖掘各大企业的商业模式，并构建出一个可检索、可计算、可推理的知识图谱。

随着项目的推进，该知识图谱中将包含中国所有上市企业历年的产品、合作关系、竞争关系、销售模式、客户关系等数据，并从中归纳出每一家企业的商业模式的变更以及所属行业的变迁。

下图是部分计划挖掘出的企业商业模式内容。

![alt 属性文本](https://github.com/Shawn91/Quantify-Business-Model/blob/main/statics/map.png?raw=true)

# 2. 已开源数据

仓库内的 `business_model_data.zip` 文件包含了本项目对2019年-2021年各大公司年报的挖掘结果。zip 包内含一份 Graphml 格式的数据，可导入 Neo4j 数据库中查看，亦可使用 igraph 等软件查看。

目前已挖掘到的数据主要包括各大企业、以及企业与政府部门之间的各种形式的合作关系。

下图是北京八亿时空液晶科技股份有限公司2020年年报中挖掘出的部分合作关系

![](https://github.com/Shawn91/Quantify-Business-Model/blob/b3c1c341b33d155663355cba6005689201200649/statics/screen_shot.jpg?raw=true)

## 2.1 关系

数据集中的合作类型关系有：

- `partner_relation`：合作关系，即除以下合作关系外的任意形式合作关系。

- `strategic_partner_relation`：战略合作关系。

- `supplier_relation`：供应商关系。有方向的关系，A -[supplier_relation]->B 表示 A 是 B 的供应商，B 是 A 的客户。

- `candidate_supplier_relation`：潜在供应商关系。有方向的关系，A -[candidate_supplier_relation]->B 表示 A 是 B 的潜在供应商，即 A 已经获取了 B 的供应商资格，但双方可能没有签订具体的供应合同。

- `dealer_relation`：经销商关系。有方向的关系，A -[dealer_relation]->B， 表示 A 是 B 的经销商。

- `agent_relation`：代理商关系。有方向的关系，A -[agent_relation]->B，表示 A 是 B 的代理商。

- `investee_relation`: 被投资关系。有方向的关系，A -[investee_relation]->B，表示 B 持有 A 的股份，但持股比例大概率不足 50%，否则 A 可能就是 B 的子公司了。

- `subsidiary_relation`：子公司关系。有方向的关系，A -[subsidiary_relation]->B，表示 A 是 B 的子公司，未必是 100% 持股的全资子公司，但至少应该是控股子公司（持股超过 50%）。

此外，数据集中还有一个 `same_to_relation`表示别名关系，如 `京东方 -[same_to_relation]->京东方科技集团股份有限公司`，说明`京东方`是`京东方科技集团股份有限公司`的别名。

另外还有一个 `disclosed_by_relation`，用于连接表示年报的 `Report` 节点与公司节点 `Company`，用于说明每一份年报是哪家公司公布的。

## 2.2 节点

目前项目中有两个核心 labels `Report` 和 `AnyOrganization`。其中 Report 表示一家公司某一年的年报，`AnyOrganization` 表示一个组织机构节点。

任意一个组织机构，往往除了 `AnyOrganization` 还会有其他 labels，在现阶段都没啥大用。是为了未来数据更丰富、识别能力更强时提前所做的设计。

此处所谓 label 是 Neo4j 这个图数据库中的概念，可以简单理解为一个 label 就是一个节点的 tag，一个节点可以有多个 labels/tags。

# 3. 项目进度

## 3.1 代码层面

本项目已经完成一个初具雏形的数据挖掘框架，并实现了企业间多种形式的合作关系的挖掘代码。

## 3.2 数据层面

本项目下载了中国所有上市企业在 2019 年、2020 年、2021 年（部分）的年报，共10000+份，并从中挖掘了年报中所记载的企业间各种形式的合作关系，并在本项目的 Github 仓库中开源了这些数据。

## 3.3 数据展示

为方便大家查看并利用相关数据，计划将组建一个网站，用于检索并可视化展示数据。预计未来几周内上线。

# 
