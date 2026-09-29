# 发布说明（Release v0.9.15-restyle.1）

## 这是什么

[EternalNight996/memory-eternal](https://github.com/EternalNight996/memory-eternal) 的**界面重构衍生版**。
原作者 **EternalNight996**，遵循 **MIT License**（`LICENSE` 原文与版权行保留未动）。

本版**只改动客户端 UI 层**，host 逻辑（`index.js`、`lib/*`）与数据格式未作任何修改——沉淀、蒸馏、`memory_recall` 召回、知识图谱、审核中心、多 Vault、MCP 挂载全部行为照旧。

## 本次改动

| 文件 | 改动量 |
|---|---|
| `src/client/index.tsx` | +423 / −291 |
| `src/client/markdown.js` | +24 / −22 |
| `web/index.html` | +53 / −19 |
| `tests/markdown.test.mjs` | +12 / −12 |

要点：

- **设计 token 全量对齐 DSH 官方**：主色 `#4176e6`、边框 4/10/12% 黑、圆角 8/12/16、阴影收敛；独立 web 页原先自带的一套旧 Tailwind 色板（`#1f2937`/`#e5e7eb`/`#3b82f6`）已替换为 DSH 官方浅色与深色两套 token
- **主布局**：大纲式侧栏（分组 + 计数徽标 + 品牌头）、页头动作组、进度条式指标、下划线搜索、pill 筛选、bento 卡片（首卡跨 2×2、`grid-auto-flow: dense` 无空格）
- **侧边栏入口**：橙色渐变 SVG → 与官方「应用中枢」同款行（36px、9px 圆角、16px 几何符号 `▤`、`--dsw-alias-interactive-bg-hover`）
- **弹窗控制**：26px 半透明浮条 → 48px 标题条 + 34px SVG 图标按钮（不遮挡内容、不与窗口控制按钮混淆）
- **正文排版**：去 emoji，改 CSS 色点与色条；列表圆点转中性色
- **深色主题**：主按钮改用 `--dsw-alias-label-primary-inverted`，修复「浅蓝底 + 白字」对比不足
- **测试**：`markdown` 7/7、`graph-lod` 5/5 通过

## 安装

```bash
# 方式一：从本仓库安装（DSH 桌面版 profile 名为 desktop）
dsh plugin --profile desktop add github:07vvvv/memory-eternal-ui-restyle

# 方式二：解压附件后本地装配
tar -xzf memory-eternal-ui-restyle-0.9.15.tgz
cd memory-eternal && node build.mjs   # 重建 lib/client.js 与 web/app.js
```

## 附件

`memory-eternal-ui-restyle-0.9.15.tgz` —— 源码包（不含 `node_modules`），解压后执行 `node build.mjs` 即可重建客户端产物。

## 截图

见仓库 `docs/showcase/`：浅色知识卡、深色主题、卡片阅读器、侧边栏入口对照、弹窗标题条。
