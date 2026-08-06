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

CLI（Rust）已完成分化：业务域全部移除，收敛为五个职能域命令，并新增知识提炼链路。这是分化期的形态：

| 类别 | 命令 | 内容 |
|------|------|------|
| 职能域 | asset | archive 日志归档、status 结构合规检查、quality 语义质量评估 |
| 职能域 | business | quote 报价、status 状态 |
| 职能域 | connect | notice 飞书群通知、chat 跨群聊天记录搜索（lark-cli im） |
| 职能域 | human | status 招聘计划与进度、position 岗位管理 |
| 职能域 | knowl | acquire LLM 知识提取、extract 本体抽取（含 policy 类型与状态承载）、summary 按主题总结现有知识 |

原业务域命令（qtclass、qtcloud、qtconsult、qtdata、qtrecurit）已全部移除，归位各平台仓库；project、share 已移除（share 迁至 devops 实验室）。CLI 已拆分为 lib + bin，领域层（connect、knowl、human）可被示例与其他消费者引用。

示例（`examples/qtrecurit.rs`、`examples/qtclass.rs`）演示完整知识链路：connect 跨群搜索聊天记录 → acquire 提取政策 → extract 本体抽取（含状态承载）→ summary 按主题总结，产物落在 `src/cli/data/`（本地承载）。

Provider 为 Go，处于维护态。Studio 为 Flutter，采用 qtadmin-org 与 qtadmin-qtconsult 分包，但页面目录为空，双端数据共享未落地。

## 差距分析

- **分化已执行**：业务域移回各平台已完成（qtdata、qtrecurit 等平台已有独立 CLI），connect 从邮件扩展出聊天记录搜索，「从飞书数据开始」的起步路径已部分落地
- **职能域堆砌了领域知识**：human、asset 等职能的规则和数据定义应继续沉淀到领域层（档案与规格），CLI 只做执行；当前仍有领域知识直接编码在命令中
- **三支柱只覆盖一角**：asset 有 archive、status、quality 三个子命令，knowl 知识链路已成型；delib（议事）与 strategy（战略）仍零实现。两者都不缺制度素材：议事制度已有完整设计（提案权下放全体、代表审议投票、会前核心小组检查）；战略推演方法论已在洞察库沉淀（`data/insight/strategy`），缺的都是系统侧载体
- **治理可视化是空的**：Studio 页面目录为空，治理思想「以系统化的方式被展示和执行」没有落地
- **workspace 缺失**：意图要求每一个人一个 workspace，CLI 是本地文件操作，无多用户、无 workspace 概念

## 行动建议

qtadmin 应沿着「集中、分化、连接」的路径迁移，最终只保留跨业务、跨职能的交叉编排点。

- **分化：业务域移回各平台**：已完成（qtclass、qtcloud、qtconsult、qtdata、qtrecurit 已从 CLI 移除）
- **分化：职能域下沉领域层**：进行中。knowl 知识链路（acquire/extract/summary）已成型；human、asset、connect 的规则与数据定义继续沉淀到领域档案和规格层，CLI 只保留执行入口
- **连接：聚焦领域交叉**：只保留需要编排多个领域能力的交叉点，例如「产教融合」把各平台工作整合成学习进度，这是管理后台区别于各平台的价值所在
- **补齐 strategy 载体**：把战略洞察（方向、张力、假设库）结构化，作为 strategy 支柱的起点。路径可先做战略第二大脑（事实审计加反事实推演），再逐渐把云聚出来，平台可先用 site 所见即所得验证
- **补齐 delib 载体**：议事制度设计已在运转（提案权下放、会前核心小组检查），直接封装为议事记录与决策留痕的最小闭环
- **封装边界**：AI 产出必须可落地，落不了地的产出是债务，不进入封装；知识承载以状态区分（settled/evolving/draft），模糊是演进中的合法承载状态，不强制澄清
- **Studio 从 asset 起步**：先做资产治理的可视化，读取 CLI 数据文件实现双端共享，再扩展其他支柱
