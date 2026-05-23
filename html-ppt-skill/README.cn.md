# html-ppt — 本项目使用说明

> 本仓库中的 `html-ppt-skill/` 是 [lewislulu/html-ppt-skill](https://github.com/lewislulu/html-ppt-skill) 的本地化副本（MIT 许可），作为运行时被本项目中的三份 HTML 演示文稿共同依赖。
>
> **本目录上游文档：** 英文 [README.md](README.md) · 中文 [README.zh-CN.md](README.zh-CN.md)
>
> **本文件：** 本项目自身的中文使用说明（与上游 README 互补，专注于本项目特有的三份演示文稿）。

---

## 三份演示文稿

本项目围绕『Agent 框架工程』这一主题，构建了三份相互呼应的演示文稿。每份都是一个自包含的 `main.html`，通过 `../../html-ppt-skill/assets/...` 加载本目录中的样式与脚本，并共享上一级目录中的 `../anthropic.css` 主题。

| 文稿 | 主题 | 打开方式 |
| --- | --- | --- |
| [`presentation/harness-LR/main.html`](../presentation/harness-LR/main.html) | 智能体框架工程的学术综述（Li et al., TMLR 2026）—— 英文版，17 张幻灯片 | `open presentation/harness-LR/main.html` |
| [`presentation/harness-LR/main-cn.html`](../presentation/harness-LR/main-cn.html) | 同上 —— 中文版（保留 `harness` 不译，并新增『词源』一页） | `open presentation/harness-LR/main-cn.html` |
| [`presentation/harness-anthropic/main.html`](../presentation/harness-anthropic/main.html) | **Anthropic 实践者视角**，综合三篇 Anthropic Engineering 博文 —— 英文版，16 张幻灯片 | `open presentation/harness-anthropic/main.html` |

## 键盘操作

| 按键 | 功能 |
| --- | --- |
| `←` / `→` / `Space` | 翻页 |
| `Home` / `End` | 首页 / 末页 |
| `N` | 演讲者备注抽屉（仅显示当前页备注） |
| `S` | 演讲者模式（独立窗口，含计时器与逐字稿） |
| `T` | 主题循环（本项目仅安装一个主题，按 `T` 不会切换） |
| `F` | 全屏 |
| `O` | 总览（如已加载） |

## 设计语言与字体

三份文稿共用一套配色与排版：

- **配色：** Anthropic 暖色调色板 —— 象牙白底色（`#FAFAF7`）、石板灰文字（`#141413`）、Book Cloth 砖红强调色（`#CC785C`）。完整调色板见 [`presentation/deck-skill/reference/palette.md`](../presentation/deck-skill/reference/palette.md)。
- **字体：** 英文正文 Charter（macOS / iOS 自带）+ 系统无衬线（San Francisco / Segoe UI）作为标题与界面元素。中文回落到苹方（PingFang SC）/ 宋体（Songti SC）。无外部 webfont 依赖，速度更快。
- **版式：** 类型驱动而非卡片驱动 —— 悬挂数字、首字下沉、行内引语、大数字、词典式条目、整版引言、英雄图等十种版式互相轮换，避免每页都长得一样。完整版式手册见 [`presentation/deck-skill/reference/patterns.md`](../presentation/deck-skill/reference/patterns.md)。

## 在这套技能之上构建新的演示文稿

如需为新论文、新文章或新主题构建演示文稿，按以下步骤：

1. 阅读工作流配方：[`presentation/deck-skill/SKILL.md`](../presentation/deck-skill/SKILL.md) —— 描述了从一份或多份 PDF / 网页到一份 15-17 页 HTML 演示文稿的完整流程。
2. 参考调色板与版式：
   - [`presentation/deck-skill/reference/palette.md`](../presentation/deck-skill/reference/palette.md)
   - [`presentation/deck-skill/reference/patterns.md`](../presentation/deck-skill/reference/patterns.md)
3. 复制模板作为起点：
   - [`presentation/deck-skill/templates/main.html`](../presentation/deck-skill/templates/main.html) —— 五页样例骨架
   - [`presentation/deck-skill/templates/anthropic.css`](../presentation/deck-skill/templates/anthropic.css) —— Anthropic 主题
4. 注意已知陷阱：[`presentation/deck-skill/reference/gotchas.md`](../presentation/deck-skill/reference/gotchas.md) —— 包含幻灯片溢出、CJK 字符间距、动画冲突等常见问题与解法。

## 关于 html-ppt-skill 本身

`html-ppt-skill` 提供：
- 36 个主题（位于 `assets/themes/*.css`）
- 31 个单页布局（位于 `templates/single-page/*.html`）
- 15 个完整演示文稿模板（位于 `templates/full-decks/<name>/`）
- 27 个 CSS 动画 + 20 个 Canvas FX 动画
- 演讲者模式（按 `S` 唤起）

本项目仅使用其运行时（`runtime.js`、`base.css`、`fonts.css`、`animations.css`），主题与版式均自定义。如需使用上游附带的主题与版式资源，详见英文 [README.md](README.md) 或中文 [README.zh-CN.md](README.zh-CN.md)。

## 许可

`html-ppt-skill/` 部分采用 MIT 许可（© 2026 lewis &lt;sudolewis@gmail.com&gt;），本项目其余部分见 [`/LICENSE`](../LICENSE)（如存在）或 [项目 README](../README.md)。
