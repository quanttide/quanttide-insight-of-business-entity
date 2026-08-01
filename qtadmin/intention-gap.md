# 量潮管理后台意图实现差距

对比管理后台意图（`data/intention/qtadmin`）与 qtadmin 应用实现，判断现有代码是否支撑治理思想平台化。差距的总根源是阶段不同步：实现停留在集中期，意图已走向连接期（见 [先集中后分化再连接](./concentrate-diverge-connect.md)）。

## 意图要求

量潮管理后台是企业治理思想和制度的平台化，展示的不是功能，是治理方法。

- 定位：不再是管理系统的集合，不再是「大杂烩」；承载量潮的治理思想，与量潮云的生产工具彻底分开
- 三支柱：delib 议事设计、strategy 战略发现、asset 资产管理
- 封装独特思考方式：从实际流程中提取模式，找到对应数据，让 AI 学习，设计程序封装
- 内部资产三层建模：来自平台的原始数据定义为 assets，人类操作分析的部分定义为 data，总结的信息和知识定义为 docs
- 起步路径：从导出飞书和 GitHub 的数据开始，建立组织层面的分析工具
- 演进方向：优惠券和代金券是未来代币的前身

## 实现现状

CLI（Rust）当前有十二个领域命令，覆盖全部业务域和部分职能域。这是集中期的形态，用广度试探深度：

| 类别 | 命令 | 内容 |
|------|------|------|
| 职能域 | asset | archive 日志归档、status 结构合规检查、quality 语义质量评估 |
| 职能域 | human | status 招聘计划与进度 |
| 职能域 | connect | email 邮件通道（lark-cli） |
| 职能域 | business | quote 报价、status 状态 |
| 职能域 | project | 项目状态 |
| 职能域 | knowl | acquire LLM 知识获取、extract 本体抽取 |
| 职能域 | share | 代码脱敏发布 |
| 业务域 | qtclass、qtcloud、qtconsult、qtdata、qtrecurit | 各业务状态查询 |

Provider 为 Go，处于维护态。Studio 为 Flutter，采用 qtadmin-org 与 qtadmin-qtconsult 分包，但页面目录为空，双端数据共享未落地。

## 差距分析

- **阶段不同步**：十二个领域命令是集中期的正常形态，用广度试探深度不是设计错误；问题是领域分化后没有跟着迁移，实现停在了集中期
- **业务域收拢是多余的**：qtclass、qtcloud、qtconsult、qtdata、qtrecurit 的状态查询属于各自平台的职责，qtdata 与 qtrecurit 已有独立 CLI，不应在管理后台重复收拢
- **职能域堆砌了领域知识**：human、asset 等职能的规则和数据定义应沉淀到领域层（档案与规格），CLI 只做执行；当前把领域知识直接编码成命令
- **三支柱只覆盖一角**：asset 有 archive、status、quality 三个子命令，delib（议事）与 strategy（战略）零实现。而战略洞察在洞察库已有沉淀（`data/insight/strategy`），缺的正是系统侧的载体
- **治理可视化是空的**：Studio 页面目录为空，治理思想「以系统化的方式被展示和执行」没有落地
- **起步路径未实现**：意图要求从导出飞书和 GitHub 数据开始，connect 目前只有邮件通道，没有飞书、GitHub 数据导出与分析
- **workspace 缺失**：意图要求每一个人一个 workspace，CLI 是本地文件操作，无多用户、无 workspace 概念

## 行动建议

qtadmin 应沿着「集中、分化、连接」的路径迁移，最终只保留跨业务、跨职能的交叉编排点。

- **分化：业务域移回各平台**：qtclass、qtcloud、qtconsult、qtdata、qtrecurit 的状态能力移回各自仓库，与管理后台解耦
- **分化：职能域下沉领域层**：human、asset、connect 等职能的规则与数据定义沉淀到领域档案和规格层，CLI 只保留执行入口
- **连接：聚焦领域交叉**：只保留需要编排多个领域能力的交叉点，例如「产教融合」把各平台工作整合成学习进度，这是管理后台区别于各平台的价值所在
- **补齐 strategy 载体**：把战略洞察（方向、张力、假设库）结构化，作为 strategy 支柱的起点
- **补齐 delib 载体**：先做议事记录与决策留痕的最小闭环
- **Studio 从 asset 起步**：先做资产治理的可视化，读取 CLI 数据文件实现双端共享，再扩展其他支柱
