# DSH Coding Workflow

一个 DeepSeek Harness 编程工作流模式预设，用于更好地约束LLM进行编程工作。

## 安装位置（以Mac桌面端DSH为例）

```
~/Library/Application Support/dsh-desktop/harness/.agent-presets/coding-workflow/
├── agent.cordis.yml              # 组合文件：standard 副本 + 工作流 persona + 预设内技能目录
├── preset.yml                    # 展示元数据：name=编程工作流 + description
└── skills/coding-workflow/SKILL.md   # 三阶段详细规程（文档模板 / 追问纪律 / 门槛话术）
```

## 说明
* 该预设通过 `需求` -> `计划` -> `实施` 三个阶段递进式约束LLM推进工作，使其严格按照规划实施编程任务，避免LLM幻觉导致计划跑偏。
* 各阶段产出文档存放于：工作区的 `Agents/{任务名称}` 文件夹下，共4个文件，分别是：
  * S1_DEMAND.md 需求文档，记录用户原始需求以及与用户的问答记录。
  * S2_DESIGN.md 计划文档，依据 S1_DEMAND.md 分析工作区代码，记录详细设计方案与制定的编码计划。
  * S3_IMPLEMENT.md 实施文档，依据 S1_DEMAND.md 与 S2_DESIGN.md 按计划正式编写代码，记录关键的新增与变更点。
  * PROGRESS.md 进度文档，记录当前任务进展情况。
* 新建会话时，会先进入 `需求` 阶段，此时可将你的需求发给LLM分析，LLM可能会向你提问。全部疑问点梳理完毕后，方可决定是否进入`计划`阶段。也就是说，你需要阅读每一阶段的产出文档，核对是否有误，并决定是否进行下一阶段。