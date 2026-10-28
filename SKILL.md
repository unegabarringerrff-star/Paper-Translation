---
name: paperdrama-paper-to-drama
description: 将可读学术论文转译为有趣、可表演的中文真人竖屏短剧，并交付场景级五份 UTF-8 TXT。适用于需要保留研究事实、明确虚构边界和交接 MicroDrama 生成视频的任务；不生成逐镜分镜、人物图片、配音或平台接口文件。
---

# PaperDrama｜论文到真人竖屏场景生产包

## 目标与边界

把论文中的主要问题、发现、机制、矛盾或未知边界转成值得观看的故事。研究事实限制事实表达，不限制人物、关系、世界、冲突、后果和视觉行动的虚构强度。

默认交付面向真人、单一 9:16 竖屏。写到场景级：每场提供人物、动作、对白、声音、连续性和必须看见的信息；MicroDrama 继续拆镜、提取人物并生成参考画面。不要预制分镜 JSON、逐镜提示词、人物图片、配音文件、模型参数、平台接口或自动发布流程。

## 输入与默认值

需要读取论文全文或明确可读范围。记录标题、来源、已读页码或章节和 missing_sections；不能用摘要猜测未读方法或结果。

用户可自然语言指定世界、类型、剧情装置、人物、时长、集数、禁忌、受众、语言、画幅或戏剧强度。未指定时默认：中文、非本领域大学生、真人 9:16、戏剧强度 4；系统根据论文自主补齐创作项，并记录假设。用户明确要求某项由其决定时，合并询问缺少项一次。

用户给定的约束优先于默认预设，除非它会篡改研究事实或使交付无法成立。先尝试在不改变用户意图的前提下调整表达；仍不能兼容时，说明具体冲突，不要静默删减、改时长或降档。

## 事实底线

读取 [paper-point-selection.md](references/paper-point-selection.md)。

不得改变关键数字、单位、组别、比较对象、结果方向、显著性、因果或相关性质、核心结论及理解结论所必需的条件。论文作者的发现、论文引用的观点和虚构剧情必须分开。虚构人物、现场、阴谋、后果和世界规则不能冒充论文实验、作者经历或已获证明的现实结论。

每项主要研究主张记录 fact_id、来源位置、性质、证据状态、重要性和必要限定。覆盖所有主要研究主张及支撑条件；无关细节按需整理。没有实验、统计或未来研究时写 NOT_APPLICABLE，不填造缺失内容。

## 强度预设与用户覆盖

读取 [dramatic-intensity.md](references/dramatic-intensity.md)。强度 1–5 是完整预设，默认 4：

1. 学术还原型
2. 轻度剧情型
3. 证据驱动型
4. 强冲突短剧型
5. 极强戏剧型

预设同时安排知识覆盖、虚构尺度、人物压力、节奏、动作和声音；用户可以明确覆盖任一维度，例如“4级但完整保留关键方法”或“5级但保持现实校园”。记录预设档位、覆盖项和实际策略。覆盖后若明显偏离标准档位，应标为自定义变体，不得同时声称完全满足标准档位。

所有档位共用事实、单场独立、连续性和交接完整性底线。5级至少使一个核心发现或核心论证在实际观看内容中参与关键选择、转折或结局；只写论文标题、片尾来源或核对备注不满足要求。

## 连续流程

### 1. 读取与事实整理

建立事实表，区分研究问题、方法、结果、解释、假设、局限和引用观点。为实际剧本中的研究断言保留可核对来源和必要限定。关键事实无法核实，且影响主锚点或必要结论时，转入 BLOCKED_FOR_FACT_REVIEW。

### 2. 选择主锚点与内容去向

从论文主要内容选择一个主 Drama 锚点，最多两个服务于主锚点的辅助锚点。完成转译链：

论文事实或关系 → 机制内核 → 戏剧世界规则 → 人物选择与后果。

核心选择、主要转折或结局必须依赖论文机制；否则重新选择锚点或转译方式。

对每项主要事实记录表达方式和承载位置。表达方式可为准确直述、通俗转述、压缩或虚构隐喻；承载位置可为对白、可见行动、后期字幕或图层、辅助核对材料或正片省略。省略正片不等于删除事实记录。任何正片研究断言所需的限定，必须在可听或可见内容中就近承载，不能只放在核对备注。

### 3. 建立唯一蓝图和故事引擎

读取 [style-axes.md](references/style-axes.md)、[narrative-library.md](references/narrative-library.md)、[drama-blueprint.md](references/drama-blueprint.md) 和 [story-engine.md](references/story-engine.md)。

只创建一个实际执行的世界、人物关系和故事线。设置观众承诺、人物欲望、阻力、优势、代价、状态变化与回报。高档作品需要具体选择、合理反制与后果；低档作品可通过探究、协作或认识修正推进。不要把论文按 Introduction、Methods、Results 机械分幕。

### 4. 写完整场景

读取 [script-writing.md](references/script-writing.md)、[cinematic-tension.md](references/cinematic-tension.md) 和 [scene-handoff.md](references/scene-handoff.md)。

按场景或完整动作与对话单元拆分。每场可单独取出使用，明确出镜、画外或电话声音、仅被提及者和旁白；写清开场状态、按顺序的动作与对白、声音、结束状态、必须保留信息、后期精确文字和核对备注。

保持真人竖屏可读性：重要人物、动作和物件集中在可见竖向区域；不依赖横向群像、整面复杂图表或画面内小字。写必须看见什么，不替下游制定镜头表。

### 5. 检查与交付

读取 [quality-gates.md](references/quality-gates.md) 和 [output-schema.md](references/output-schema.md)。

事实、分档创作和交接检查通过后，交付五份 UTF-8 TXT，其中 03 是唯一默认送入 MicroDrama 的文件。已有同名产出不得静默覆盖。没有实际视频时，只能确认文本准备度。交付在文本检查通过后结束。

关键事实阻断时，不交付生产就绪的五份文件或 03；保留已整理的可靠事实与阻断清单，说明缺少的章节、页码、图表或原文。

## 参考文件

- [paper-point-selection.md](references/paper-point-selection.md)：事实边界、锚点与不可替换性。
- [dramatic-intensity.md](references/dramatic-intensity.md)：五档预设、覆盖与改档。
- [style-axes.md](references/style-axes.md)：创作维度与自然语言解析。
- [narrative-library.md](references/narrative-library.md)：可选叙事模式。
- [drama-blueprint.md](references/drama-blueprint.md)：唯一项目蓝图。
- [story-engine.md](references/story-engine.md)：人物选择、因果和回报。
- [cinematic-tension.md](references/cinematic-tension.md)：场景张力、可见行动和声音。
- [script-writing.md](references/script-writing.md)：完整场景写作与时间预算。
- [scene-handoff.md](references/scene-handoff.md)：唯一场景交接模板。
- [quality-gates.md](references/quality-gates.md)：检查与定向返工。
- [output-schema.md](references/output-schema.md)：五份 TXT 的交付合同。
- [acceptance-tests.md](tests/acceptance-tests.md)：待执行验收规范。