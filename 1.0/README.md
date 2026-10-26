# PaperDrama Skill v1.0.0

功能：论文 PDF/正文 → 结构化事实拆解 → 学术冲突候选 → Drama Blueprint → 事实-剧情溯源 → 两道审核。

## 安装到 Codex
1. 解压本包，将 `paperdrama-skill` 整个文件夹复制到 Codex 识别的 skills 目录（常见个人路径 `$HOME/.agents/skills/`；若当前环境提供其他路径，以其规范为准）。
2. 保留文件夹内的 `SKILL.md`、`references/`、`assets/`、`tests/`。
3. 在 Codex 对话输入：`请使用 paperdrama-paper-to-drama Skill，分析 @某篇论文.pdf，完成 PaperDrama 阶段1的论文拆解和转译；只输出事实库、候选冲突、Drama Blueprint 与校验文件，不写完整剧本。`
4. 运行 tests/acceptance-tests.md 的 T1–T6 复测。

## 阶段边界
此版本不生成视频、不生成完整对白、不做视频渲染；完成后可以交给后续 PaperDrama 剧本/分镜生成模块。

## 设计依据
- Carter et al. (2025), KaraokAI, CHI EA, doi:10.1145/3706599.3721113：研究四桶提取 + 歌曲结构蓝图 + 双约束生成。
- Cristobal et al. (2026), PaperTok, CHI, doi:10.1145/3772318.3790553：四项具体发现、叙事角度候选、Hook 生成/筛选、分镜结构和人机协作。

PaperDrama 的七标签、Drama Blueprint、事实等级与双重审核是从上述方法发展出的新方案，不应写成两篇论文作者已提出的方法。
