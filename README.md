# coding-workflow 预设源文件

本工作区是 DeepSeek Harness 用户预设 **`coding-workflow`（编程工作流）** 的源文件副本，与安装目录保持同步。

## 安装位置

```
~/Library/Application Support/dsh-desktop/harness/.agent-presets/coding-workflow/
├── agent.cordis.yml              # 组合文件：standard 副本 + 工作流 persona + 预设内技能目录
├── preset.yml                    # 展示元数据：name=编程工作流 + description
└── skills/coding-workflow/SKILL.md   # 三阶段详细规程（文档模板 / 追问纪律 / 门槛话术）
```

## 结构说明

- `agent.cordis.yml` 是 shipped `standard` 预设的副本，只改了两处：
  1. **persona 行**：声明三阶段流程（S1 需求 → S2 设计 → S3 实施）、会话初始化的任务定位规则、阶段门槛（Gate）与 `PROGRESS.md` 唯一事实源。
  2. **skill-filesystem 行**：追加 `customSkillDirs` 指向预设自身 `skills/` 目录，让规程随预设走。
- 详细操作规程放在 `skills/coding-workflow/SKILL.md`（按需加载），persona 只保留必须常驻上下文的骨架规则。

## 修改与同步

在本工作区改完源文件后，同步回安装目录（目标在工作区外，需要提升文件写权限）：

```sh
DST="$HOME/Library/Application Support/dsh-desktop/harness/.agent-presets/coding-workflow"
mkdir -p "$DST/skills/coding-workflow"
cp preset.yml agent.cordis.yml "$DST/"
cp skills/coding-workflow/SKILL.md "$DST/skills/coding-workflow/SKILL.md"
```

同步后在任意 Cordis 会话里用 `agentPresets.standingKeyFor('coding-workflow')` 做挂载校验（roster 的 `broken` 字段只做格式检查，不做组合校验）。

## 已知坑

- `@deepseek-ai/dsh-persona` 的配置字段是 `prefix`（必填）/ `suffix` / `includeRuntimeContext`，**没有 `text` 字段**——用 `text:` 会在挂载时报 `$.prefix missing required value`（本地 `weekly-report` 预设即踩此坑，仅供对照）。
