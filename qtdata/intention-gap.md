# 量潮数据意图实现差距

对比量潮数据意图（`data/intention/qtdata`）与 qtdata 应用实现。

## 意图要求

- 平台化终局：三方体系，客户看交付进度和成果，执行方看任务标准和收益，平台方看全貌
- 信用与定价权是平台的核心价值
- 客户资产整理是第一优先级
- 以业务邮箱为中心的沟通渠道
- 老客户维护与发券增长策略

## 实现现状

- CLI：blueprint、scope、quotation、delivery 四命令，本地读 Markdown，调 LLM 输出 JSON
- Provider：项目与任务 CRUD 骨架，无业务逻辑
- Studio：仪表盘与项目详情，数据来自 mock

## 过时点

- 产品逻辑停留在「Markdown 转 JSON」，而意图是「技术管理的执行系统」
- 客户资产、邮箱沟通、发券增长三个意图在代码中零体现
- Studio 只有客户视角的进度展示，且是 mock 数据

## 行动建议

STATUS 文档已做差距分析，按现有 roadmap 推进即可。
