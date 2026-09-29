# 衍生说明（NOTICE）

## 来源与署名

| 项 | 内容 |
|---|---|
| 原项目 | [EternalNight996/memory-eternal](https://github.com/EternalNight996/memory-eternal) |
| 原作者 | **EternalNight996** |
| 原版本 | `memory-eternal@0.9.15`（npm 包与仓库 `main` 分支，2026-09-29） |
| 许可 | MIT License（完整文本见本仓库 `LICENSE`，版权行原样保留） |
| 本衍生版 | 仅重构客户端 UI 层（界面风格对齐 DeepSeek Harness 主界面） |

MIT 许可允许修改与再分发，条件是**保留原版权声明与许可文本**。本仓库已保留 `LICENSE` 原文，并在 `README.md` 顶部与本文件标注原作者与来源。

## 改了什么

只涉及 4 个源文件（host 逻辑与数据格式零改动）：

| 文件 | 改动量 | 内容 |
|---|---|---|
| `src/client/index.tsx` | +423 / −291 | 主界面与各面板的样式与结构 |
| `src/client/markdown.js` | +24 / −22 | 卡片正文排版去 emoji，改用 CSS 色点/色条 |
| `web/index.html` | +53 / −19 | 独立 web 页色板替换为 DSH 官方设计 token |
| `tests/markdown.test.mjs` | +12 / −12 | 断言同步更新 |

构建产物随之重新生成：`lib/client.js`、`web/app.js`。

### 界面层具体改动

1. **设计 token 对齐**：主色 `--dsw-alias-state-business-primary`（#4176e6）、三级文字 `label-primary/secondary/tertiary`、
   边框 `border-l1/l2/l3`（4/10/12% 黑）、圆角 8/12/16、阴影收敛到 `0 2px 8px rgba(0,0,0,.04)` 级别；
   状态色统一用 `color-mix` 自适应深浅主题。
2. **主布局**：侧栏由可折叠图标条（含 emoji）改为 244px 大纲式导航（分组标题 + 行项 + 计数徽标 + 品牌头）；
   新增页头（标题 + 动作组）；指标改为通栏进度条式；搜索改无边框下划线；分类/排序改 pill 行。
3. **卡片**：编辑式排版（圆角 16、1px 细线、hover 抬升 1px）；状态改为低饱和 chip；
   卡片数为 3 的倍数时启用 bento（首卡跨 2×2，`grid-auto-flow: dense`，无空格）。
4. **侧边栏入口**（`sidebar.footer.action`）：原橙色渐变 SVG 图标 → 与 DSH 官方「应用中枢 / 插件市场」同款行
   （36px 高、9px 圆角、16px 几何符号 `▤`、`--dsw-alias-interactive-bg-hover` hover）。
5. **弹窗控制**：原先 26px 半透明浮条（浮在 iframe 上方、易误点）→ 48px 标题条 + 34px SVG 图标按钮。
6. **面板与正文统一**：配置页去彩色渐变左边条与标题 emoji；toast/提示条统一为状态色细条；
   阅读器元信息 chips 统一；图谱页画布去渐变、浮层跟随主题；用量页日志图标改符号。
7. **深色主题**：主按钮文字改用 `--dsw-alias-label-primary-inverted`，修复深色下对比不足。

### 未改动

- `index.js`（host 侧：沉淀、蒸馏、召回、`memory_recall` 工具、`/memory-eternal/api/*` 路由、设置 schema）
- `lib/` 下全部 host 模块（`db.js`、`vault.js`、`capture.js`、`api.js`、`watchdog.js`、`setup.js` 等）
- `cordis.patch.yml`、`package.json` 的依赖与脚本、README 正文（仅在顶部增加了本衍生说明）

## 与上游的关系

- 上游更新可直接覆盖 `src/client/`、`web/index.html`、`tests/` 之外的改动；若上游也重构了 UI，需要手动合并本文件的改动。
- 回滚到上游 UI：用上游对应版本的同名文件覆盖上述 4 个文件后重新执行 `node build.mjs`。
- 本衍生版沿用上游包名与功能语义，**不是**官方发布；请勿将其视为原作者的版本。

## 构建

```bash
npm install          # 或 pnpm i，需要 esbuild
node build.mjs       # 产出 lib/client.js（DSH 内嵌）与 web/app.js（独立 web）
node tests/markdown.test.mjs
```

## 数据与隐私

插件运行期数据（知识卡、SQLite 索引）存放在本机 `~/.dsh/memory-vault`，**不在本仓库内**，也不会随本仓库分发。
