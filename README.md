# 论文数据管线讲透

给它单篇或多篇论文，直接得到带原图、机制解释、横向比较和证据边界的中文数据管线报告。

## 一次装好：把这段提示词交给 AI

复制下面整个代码块给负责安装的 AI。它会安装 **1 个主 skill＋5 个二级 skills**，并单独检查运行工具。二级技能在写报告时按需使用，不需要你选择组合。

```text
请实际安装“论文数据管线讲透”完整套件，包含主 skill 和下面全部 5 个二级 skills，不要只给教程，也不要按名称搜索同名替代品。

唯一安装清单（repo、path、ref 缺一不可）：
- paper-pipeline-report: repo=Xiaoye119/paper-pipeline-report; path=paper-pipeline-report; ref=v1.1.0
- doc2x-cli: repo=NoEdgeAI/doc2x-cli-skills; path=skills/doc2x-cli; ref=41864e8aca014712807e9cde872cfcd90d7ac87e
- pdf: repo=anthropics/skills; path=skills/pdf; ref=e4bb5d960d87126ff3b3a8af1a104b7db67560ba
- ljg-paper: repo=lijigang/ljg-skills; path=skills/ljg-paper; ref=c84ca0d027db6442d408f1124d8553dcc6b2b29d
- doc-coauthoring: repo=anthropics/skills; path=skills/doc-coauthoring; ref=e4bb5d960d87126ff3b3a8af1a104b7db67560ba
- scientific-critical-thinking: repo=K-Dense-AI/scientific-agent-skills; path=skills/scientific-critical-thinking; ref=c21d13b3cc2894680229ba9959a53281acb9200e

执行要求：
1. Codex 安装到 $CODEX_HOME/skills，未设置则用 ~/.codex/skills；其他兼容 Agent 用其实际支持的技能目录。先识别操作系统和安装器位置，不照抄别人的本机路径。
2. 优先使用当前环境的 skill-installer/install-skill-from-github.py。逐条执行下列命令；<installer> 替换为实际脚本路径，<skills目录> 替换为目标目录。若不存在该安装器，下载指定 commit/tag 的官方仓库快照，仅复制指定技能的整个目录；保留 references、scripts、agents 和许可文件，不只取 SKILL.md，不执行仓库里不相关的安装脚本。
python <installer> --repo Xiaoye119/paper-pipeline-report --ref v1.1.0 --path paper-pipeline-report --dest <skills目录>
python <installer> --repo NoEdgeAI/doc2x-cli-skills --ref 41864e8aca014712807e9cde872cfcd90d7ac87e --path skills/doc2x-cli --dest <skills目录>
python <installer> --repo anthropics/skills --ref e4bb5d960d87126ff3b3a8af1a104b7db67560ba --path skills/pdf --dest <skills目录>
python <installer> --repo lijigang/ljg-skills --ref c84ca0d027db6442d408f1124d8553dcc6b2b29d --path skills/ljg-paper --dest <skills目录>
python <installer> --repo anthropics/skills --ref e4bb5d960d87126ff3b3a8af1a104b7db67560ba --path skills/doc-coauthoring --dest <skills目录>
python <installer> --repo K-Dense-AI/scientific-agent-skills --ref c21d13b3cc2894680229ba9959a53281acb9200e --path skills/scientific-critical-thinking --dest <skills目录>
3. 已有同名目录时先核对来源与内容，完全匹配则复用。来源不同、来源不明或本地有修改时，不静默覆盖：先将整个旧目录备份到技能发现目录之外，再安装本清单版本，并记录备份位置；受权限限制时报告具体冲突，继续安装无冲突项。
4. 读取主 skill 内 references/install-sources.json，确认它与本提示词的 repo/path/ref 一致，并校验 5 个二级 skills 的 SKILL.md SHA-256。必须安装完整目录，入口 hash 不是其他文件的校验替代。保留每项的来源、版本、目标路径与文件清单；不要将 main/latest 当成锁定的技能版本。
5. 技能文件安装完成后，单独检查运行环境。优先复用已有且可用的 Doc2X MCP；缺失时按 doc2x-cli 的官方说明检查 Node.js 和稳定版 CLI，使用 @noedgeai-org/doc2x-cli@latest（不装预发布版）。不要把安装 skill 当成安装了 CLI/MCP。缺少登录/额度/密钥时明确报告并请用户完成必要登录，不索要在聊天里粘贴密钥；不要为了验证安装上传论文或提交计费转换。缺 Doc2X 时仍可使用原文 HTML 与 PDF 核验路径。
6. 检查 Python 与 PDF 页面渲染能力；按所选辅助技能和当前平台补齐本报告工作流所需依赖。无需为可选辅助技能的其他独立模式安装整套无关工具（如 Emacs、图像生成 API）。
7. 校验 6 个技能目录的 SKILL.md 和实际支持文件；有 quick_validate.py 时运行它，并区分格式问题与宿主兼容性。最后逐项报告“已安装/复用/失败、来源、版本、校验结果”，另列“Doc2X已可用或待登录、PDF页面渲染可用或缺失”。不能把部分完成说成全部可运行。

完成后，我只需要说：用 $paper-pipeline-report 把这些论文写成带原图的数据管线详解。
```

## 精确来源，避免同名误装

完整机器可读清单与入口文件哈希见 [`install-sources.json`](paper-pipeline-report/references/install-sources.json)。以下都是指定作者的具体仓库目录，commit 固定后不随默认分支更新。升级版本应重新核验并更新清单。

| 二级 skill | 指定仓库与固定版本链接 | 安装目录（仓库内） | 固定 commit |
|---|---|---|---|
| `doc2x-cli` | [NoEdgeAI/doc2x-cli-skills](https://github.com/NoEdgeAI/doc2x-cli-skills/tree/41864e8aca014712807e9cde872cfcd90d7ac87e/skills/doc2x-cli) | `skills/doc2x-cli` | `41864e8aca014712807e9cde872cfcd90d7ac87e` |
| `pdf` | [anthropics/skills](https://github.com/anthropics/skills/tree/e4bb5d960d87126ff3b3a8af1a104b7db67560ba/skills/pdf) | `skills/pdf` | `e4bb5d960d87126ff3b3a8af1a104b7db67560ba` |
| `ljg-paper` | [lijigang/ljg-skills](https://github.com/lijigang/ljg-skills/tree/c84ca0d027db6442d408f1124d8553dcc6b2b29d/skills/ljg-paper) | `skills/ljg-paper` | `c84ca0d027db6442d408f1124d8553dcc6b2b29d` |
| `doc-coauthoring` | [anthropics/skills](https://github.com/anthropics/skills/tree/e4bb5d960d87126ff3b3a8af1a104b7db67560ba/skills/doc-coauthoring) | `skills/doc-coauthoring` | `e4bb5d960d87126ff3b3a8af1a104b7db67560ba` |
| `scientific-critical-thinking` | [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills/tree/c21d13b3cc2894680229ba9959a53281acb9200e/skills/scientific-critical-thinking) | `skills/scientific-critical-thinking` | `c21d13b3cc2894680229ba9959a53281acb9200e` |

PDF 配套项明确选用 `anthropics/skills` 的 `skills/pdf`。某些宿主自带的 `pdf:pdf` 是另一种插件能力，不能假定其他机器存在，也不把它当作这个 GitHub 依赖的别名。

本次 Doc2X skill 固定在官方仓库的新修订，区别于最初本机的旧版 skill；技能版本不代表 npm CLI 已发布对应功能。操作前按其说明核对实际 CLI 的 help 和稳定版能力。[官方安装说明](https://doc2x.noedgeai.com/help/zh-cn/faq/doc2x-cli-skills.html)也区分技能安装与 CLI 安装。

## 日常使用

```text
用 $paper-pipeline-report 把这些论文写成一份数据管线详解：
[论文链接或本地 PDF]
```

报告沿着数据变化说明来源、筛选、转换、标注和训练样本，解释每一步为什么做、处理粒度与失败分支，并比较各篇设计。工具、技能选择及读者检查由助手处理。

## 只安装主 skill

需要精简安装时，可下载 [v1.1.0 主技能安装包](https://github.com/Xiaoye119/paper-pipeline-report/releases/download/v1.1.0/paper-pipeline-report-v1.1.0.zip)，把 `paper-pipeline-report` 文件夹放入技能目录。该 ZIP **不内含第三方 skills**；要把配套项一次装齐，使用上方提示词。主技能本身可独立运行，完整套件用于把可选协作能力准备齐全。

## 验证与边界

见 [VALIDATION.md](VALIDATION.md)。技能文件、CLI/MCP 程序、服务认证和真实转换是不同层面的状态，安装提示词要求分别验收。本仓库不包含服务凭据、论文全文或第三方技能副本。
