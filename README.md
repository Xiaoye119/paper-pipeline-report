# 论文数据管线讲透

一个 Codex skill：给它单篇或多篇论文，直接得到带原图的中文数据管线报告。

```text
用 $paper-pipeline-report 把这些论文写成一份数据管线详解：
[论文链接或本地 PDF]
```

报告沿着数据变化说明来源、筛选、转换、标注和训练样本；解释每一步为什么做、处理粒度与失败分支，并比较不同论文的设计。重要公式、数字和例外回查原文；作者披露、技术解读和复现缺口分别表达。

## 安装

下载 [v1.0.0 安装包](https://github.com/Xiaoye119/paper-pipeline-report/releases/download/v1.0.0/paper-pipeline-report-v1.0.0.zip)，把其中的 `paper-pipeline-report` 文件夹放到 `~/.codex/skills/`（配置了 `CODEX_HOME` 时放到其 `skills/`）。在新会话中使用 `$paper-pipeline-report`，或直接要求“写一份论文数据管线详解”。

仓库中的可安装技能目录为 [`paper-pipeline-report/`](paper-pipeline-report/SKILL.md)。也可以把该 GitHub 目录链接交给 Codex 的 skill-installer 安装。

## 工具与辅助技能

本技能自包含。Doc2X MCP 可用时优先复用或生成结构化材料；不可用时使用原文 HTML、PDF 页面等。关键图表和公式不能只凭 OCR 定论。Doc2X 使用需要使用者自己的服务配置与额度，本仓库不包含凭据。

`ljg-paper`、`doc-coauthoring`、`scientific-critical-thinking` 等只在具体解释、结构或证据判断需要时作为可选辅助，不要求全部安装。用户无需指定组合、执行顺序或逐节确认。

有可用且允许的代理工具时，使用新上下文读者检查成稿，再修订误解；否则明确标记为自检。交付包括报告和实际引用图片，不用解析文件或技能评分代替成稿。

## 验证与边界

见 [VALIDATION.md](VALIDATION.md)。格式校验与一次实际试写不能保证任意论文都无误。图文渲染取决于阅读器；公开论文全文和图像的再发布还须遵守其各自许可。本仓库仅发布技能和验证摘要，不附带论文材料或第三方技能全文。
