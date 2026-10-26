# PaperDrama — Academic PDF to Complete Drama Script Skill (v2.0.0)

**将一篇学术论文改编为完整、逐集可拍的 Drama 短剧脚本，并保留学术事实溯源。** 直接在 GitHub main 分支维护，不使用版本目录。

## 最简使用方式
在 Codex 的环境中安装本 Skill，**只上传 PDF 并调用** `paperdrama-paper-to-drama`，无需提供关键词或完整提示词：

**第一轮：** Skill 自动读取论文 → 建立学术事实库 → 找戏剧化机会 → 匹配 Drama Blueprint → **当场展示恰好 3 种不同的短剧叙事模板（A/B/C）**，包括角色、冲突、Hook、剧情路线、建议集数和每集时长。**此处必须等待用户选择**，不会擅自挑选生成最终稿。

**第二轮：** 用户回复 `A`、`B`、`C` 或“选第二套”等，Skill 复用先前分析结果，自动写完**所有集的完整分集、场景、镜头、对白、动作、音效及字幕**，审查后输出 `full_script.md`、`series_outline.md`、`quality_report.md` 和结构化元数据。

**集数和每集时长按实际论文学术节点与剧情密度规划**，不固定三集，不照搬 PaperTok 的短视频镜头数与表达方式。

## 执行路线
```
PDF论文 → 学术事实库
        → 戏剧化机会（反常识/争议/实验悬念/转折等）
        → Drama Blueprint（类型/角色/冲突/集数/节奏/表演规则）
        → 3套候选剧情 A/B/C →【等待用户选择】
        → 分集大纲 → 场景 → 完整对白 → 镜头/动作/音效/字幕
        → 学术核验 + 戏剧核验 + 时长核验
        → 全集完整脚本 full_script.md
```

## 安装
克隆/下载本仓库，将包含 `SKILL.md`、`references/`、`tests/` 和 `assets/` 的完整目录放入支持技能加载的 Codex Skills 路径（如个人环境的 `~/.agents/skills/paperdrama-paper-to-drama/`；具体取决于宿主配置）。按宿主说明重新加载/发现技能。

## 交付文件
- 阶段 A：`paper_facts.md`、`dramatic_opportunities.md`、`drama_blueprints.md`、`template_options.md`、`traceability_matrix.md`、`paperdrama.json`。
- 阶段 B：`series_outline.md`、**`full_script.md`**、`quality_report.md`；同时更新事实追溯和 JSON；可选 `full_script.json`。
- 所有文件按论文独立放在 `outputs/<论文文件名>/`；现存文件不静默覆盖。

## 理论参考与创新界限
- KaraokAI (CHI EA 2025, DOI: 10.1145/3706599.3721113)：学术提取结果与歌曲形式结构独立预处理、联合约束生成。
- PaperTok (CHI 2026, DOI: 10.1145/3772318.3790553)：参考其**流程组织**——选择核心研究内容、产生多个叙事入口、人工选择和编辑、生成脚本与媒介单元、逐步调整。**不复用其科普语气、固定8镜头/45秒或 TikTok 式画面。**
- “三套短剧叙事模板门槛”“Drama Blueprint”“人物行动映射”“镜头—原文事实映射”是 PaperDrama 的独立方案，非前两篇论文的原系统功能。

## 版本更新
- **v2.0**：从只生成论文拆解/蓝图，扩展至选定模板后的完整短剧脚本；增加必选3模板、完整对白与逐镜分镜、集数及每集时长、事实/叙事/制作三道检查。
- v1.1：调用 Skill + PDF 零关键词完成论文拆解与转译；保留原则，但现在新增一次必要的创作选择。
- v1.0：论文事实提取、戏剧机会与蓝图。

## 复测
详见 `tests/acceptance-tests.md`。仅确认 GitHub 文件写入不代表已通过真实 PDF + 两轮交互的端到端测试。
