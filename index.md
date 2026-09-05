# 意图与实现差距分析

对比数据意图（`data/intention`）与各应用实现（`apps`），判断应用代码是否落后于战略意图。

意图是「未来的自我记忆」，相对前瞻；应用实现是历史沉淀。过时的本质是代码没有跟上意图的演进，而不是代码写错。

> 公司级定位文档：[intro/institution-innovation-lab.md](intro/institution-innovation-lab.md)——制度创新实验室（横跨所有业务域的组织定位，不在任何 qt 业务目录之下）

## 过时的两种形态

- **落后型**：方向正确，深度不够。实现的是意图旧阶段的一个切片，需要补功能
- **错位型**：方向本身跑偏。实现的概念在意图中不存在，或与意图明确否定的方向一致

## 全景

| 应用 | 意图核心 | 实现现状 | 过时判断 |
|------|---------|---------|---------|
| qtcloud | 五大云：资产、执行、写作、客服、创新 | CLI 空壳，Studio 事件契约三屏静态数据 | 错位 |
| qtclass | 学生为中心的自学平台 | 课表、课堂、点名 | 错位 |
| qtdata | 平台化、三方体系、客户资产第一优先级 | CLI 本地单用户，Studio mock 看板 | 落后 |
| qtadmin | 治理思想平台化 | CLI 十二领域命令，Studio 页面为空 | 错位 |
| qtrecurit | 序列轨道与考核标准 | 邮件漏斗统计 | 落后 |

## 结构性缺口

- **有意图无实现**：qtdata 的客户资产、邮箱沟通、发券增长三个意图没有代码承接

## 行动建议

- qtcloud 与 qtclass 风险最高，现有代码方向会持续误导后续开发，先对齐产品概念再补功能
- qtdata 已有 STATUS 差距分析，按 roadmap 推进即可
- 各应用细节见各域文件夹的 [intention-gap](./qtdata/intention-gap.md) 文档

## 洞察分流说明

本仓库部分领域洞察已分流至对应领域洞察子仓库（非 qt 开头的领域级洞察）：

| 原目录 | 分流目标 |
|--------|---------|
| `org/` | quanttide-insight-of-organization-management |
| `strategy/` | quanttide-insight-of-strategy-management |
| `asset/` | quanttide-insight-of-asset-management |
| `connect/` | quanttide-insight-of-communication-management |
| `knowl/` | quanttide-insight-of-knowledge-engineering |
| `business/` | quanttide-insight-of-business-development |
| `delib/` | quanttide-insight-of-deliberation-management |

本仓库保留：业务域洞察（`qtcloud/`、`qtclass/`、`qtdata/`、`qtadmin/`、`qtrecurit/`）与本文件（意图差距全景分析）。
