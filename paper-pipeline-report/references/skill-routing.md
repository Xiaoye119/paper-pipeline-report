# 可选辅助技能：助手内部选择

完整套件安装时，按照 [install-sources.json](install-sources.json) 安装全部 5 个二级 skills；仓库 README 提供可直接交给安装 AI 的完整提示词。清单固定每项的作者/仓库、目录、commit 与 SKILL.md 哈希，不能按名称搜索同名替代品。

报告执行时，需要下列具体帮助才读取已安装的 SKILL.md。技能名不是可执行函数；“调用”指读取指令并完成相关工作，或将明确子任务交给代理。缺失项不应被假称已调用；可用主技能完成的部分继续处理。安装全部配套技能与每次全部运行，是两件事。

| 需要 | 可选技能 | 本任务采用的部分 |
|---|---|---|
| Doc2X 结构化解析 | `NoEdgeAI/doc2x-cli-skills` → `skills/doc2x-cli` | 已连接 MCP 优先于另装 CLI；串行、任务复用。技能文件不等于 CLI/MCP 服务；使用 CLI 时按官方说明检查稳定版实际能力及认证。 |
| PDF 提图和页面核对 | `anthropics/skills` → `skills/pdf` | 保留原页证据；不以文本抽取替代图表和公式核验。宿主若另有 `pdf:pdf` 可使用，但它不是此安装项的别名或前提。 |
| 解释术语化、单篇贡献不清 | `lijigang/ljg-skills` → `skills/ljg-paper` | 具体对象与动作、研究贡献、证据如何支持判断。请求改写相关解释，不额外引入笔记目录、Denote、Emacs 等无关交付体系。 |
| 多篇结构松散、读者自行拼接 | `anthropics/skills` → `skills/doc-coauthoring` | 结构精炼和新上下文读者测试。本任务采用一次成稿并自动检查，不启用逐节征询、选题菜单或反复审批。 |
| 实验结论或归因边界不清 | `K-Dense-AI/scientific-agent-skills` → `skills/scientific-critical-thinking` | 比较条件、混杂因素、实验单位和适用范围，不默认套医学评级或给每篇总分。 |

这些不是每次必跑的固定顺序。需要某辅助技能的完整独立产物时再明确该子任务；其格式约定与用户要求不同时保持用户要求。遵守实际使用资源的许可与署名，不复制打包辅助技能全文。
