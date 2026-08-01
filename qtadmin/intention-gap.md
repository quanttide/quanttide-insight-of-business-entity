# 量潮管理后台意图实现差距

对比管理后台意图（`data/intention/qtadmin`）与 qtadmin 应用实现。

## 意图要求

- 治理思想的平台化，不再是功能的大杂烩
- 三支柱：delib 议事、strategy 战略、asset 资产管理
- 内部资产三层建模：assets、data、docs
- 起步路径：从导出飞书和 GitHub 数据开始

## 实现现状

- CLI：asset、human、connect 等十二个领域命令
- Provider：Go，维护态
- Studio：页面目录为空，双端数据共享未落地

## 过时点

- 十二个领域命令的集合形态，正是意图否定的「大杂烩」
- 三支柱只覆盖 asset，delib 与 strategy 无实现
- 治理思想的可视化展示是空的

## 行动建议

收缩 CLI 命令集合，优先补齐 delib 与 strategy 的载体。
