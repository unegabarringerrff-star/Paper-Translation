# PaperDrama Skill v1.1.0

功能：论文 PDF/正文 → 结构化事实拆解 → 学术冲突候选 → Drama Blueprint → 事实-剧情溯源 → 两道审核。

## 安装到 Codex
1. 解压本包，将 `paperdrama-skill` 整个文件夹复制到 Codex 识别的 skills 目录（常见个人路径 `$HOME/.agents/skills/`；若当前环境提供其他路径，以其规范为准）。
2. 保留文件夹内的 `SKILL.md`、`references/`、`assets/`、`tests/`。
3. 上传或附上论文 PDF 后，在 Codex 中**直接调用** `paperdrama-paper-to-drama` Skill 即可；不用再写任何“拆分、转译”等关键词或补充提示词。Skill 将自行使用默认参数完成阶段 1，并将 6 个文件保存至 `outputs/<论文文件名>/`。如果宿主支持自动意图匹配且任务意图明确，也可自动匹配；单纯上传 PDF 并不保证宿主一定触发。
4. 运行 tests/acceptance-tests.md 的 T1–T6 复测。

## 阶段边界
此版本不生成视频、不生成完整对白、不做视频渲染；完成后可以交给后续 PaperDrama 剧本/分镜生成模块。

## 设计依据
- Carter et al. (2025), KaraokAI, CHI EA, doi:10.1145/3706599.3721113：研究四桶提取 + 歌曲结构蓝图 + 双约束生成。
- Cristobal et al. (2026), PaperTok, CHI, doi:10.1145/3772318.3790553：四项具体发现、叙事角度候选、Hook 生成/筛选、分镜结构和人机协作。

PaperDrama 的七标签、Drama Blueprint、事实等级与双重审核是从上述方法发展出的新方案，不应写成两篇论文作者已提出的方法。

## v1.1 更新：PDF + 调用 Skill 即自动执行
- 新增零关键词入口、自动寻找当前可访问 PDF、默认受众/剧种/集数/输出目录。
- 多份 PDF 默认逐篇独立处理；不再逐步询问无关参数。
- 即使需要人工最终审批，也会先交付第一阶段完整结果。
- 保留事实证据溯源、学术边界与双审查规则。
- 复测：见 tests/acceptance-tests.md 的 T7–T10。
