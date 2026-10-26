# Drama Blueprint｜论文内容与短剧表演的双结构转译（v2.2）

本文件是 `SKILL.md` 阶段 A 的**必读约束**，用于建立可执行的 Drama Blueprint 和对应的学术事实追溯。其六类表演语法与八类论文—Drama 映射是 PaperDrama 的设计方法，不宣称来自 KaraokAI 或 PaperTok 的原文方法。

## 1. 论文端：建立可追溯的语义结构
保留 `motivation / method / finding / contribution` 四个通用桶，并按具体内容补充研究问题、知识缺口、假设、研究行动、证据、结论、局限、后续研究等标签。每条学术事实都记录 `fact_id`、原文页码/章节/表图、限定词、信息等级（`A_CORE` / `B_COMPRESSIBLE`）及可供角色表演的解释方式。不要在缺少数据或来源的情况下假定有真实实验、观点之争或明确未来研究计划。

## 2. Drama 端：六类表演语法（每个内部 Blueprint 必须实例化）

| Drama 表演要素 | 给 AI 的结构化约束 | 内部字段 | 内容检查 |
|---|---|---|---|
| **人物** | 角色数量、身份、目标、性格、人物关系 | `characters.count / characters.roles[].identity / goal / personality / relationships` | 每个主要角色都能说清楚想要什么；真实论文作者/被试不得被冒充 |
| **冲突** | 双方诉求、阻碍、矛盾升级方式 | `conflict.opposing_demands / obstacles / escalation` | 双方诉求可由虚构角色代理，但学术观点/矛盾必须真实、可溯源 |
| **情节** | 起因、行动、意外、高潮、结果 | `plot.inciting_incident / actions / surprise / climax / outcome` | 行动与结果存在因果；没有真实意外结果时，意外可以是人物误解被纠正，不能变造数据 |
| **情绪** | 好奇、紧张、怀疑、惊讶、释然 | `emotion.emotional_beats[]` | 这些是可用情绪节点，不必强行按此顺序或集齐五类；标注对应剧情节点 |
| **表演** | 对白语气、停顿、动作、表情、镜头 | `performance.dialogue_tone / pauses / actions / expressions / camera` | 能成为具体可演动作/镜头，不应退化成三个人轮流念论文 |
| **节奏** | 前几秒的钩子、关键转折点、集尾悬念 | `rhythm.opening_hook / turning_points / episode_cliffhangers` | 开场可在数秒内建立悬念；集尾不能靠伪造科学结论制造悬念 |

**每套内部蓝图的强制检查**：上表六个顶层类别都必须有具体内容；任何字段如论文不支持，应明确写 `NOT_APPLICABLE` 并解释，不可擅自填入“真实发生”。角色、舞台和情绪可以虚构但必须按 `FICTIONAL_DEVICE` 标记，并确保核心科学主张有 `fact_ids`。

## 3. 论文内容与 Drama 情节的八类对应关系（核心转译表）

| 论文内容 | Drama 情节 | 对应表演方式 | 转译原则 |
|---|---|---|---|
| **研究背景** | 主角陷入困境 | 用具体事件开场 | 可虚构情境，不能虚构研究结论 |
| **文献争议** | 双方观点对立 | 争论、对峙、辩论 | 保留原始争议的真实含义；没有争议时不编造 |
| **研究假设** | 主角提出大胆想法 | 宣言、约定、挑战 | 不把假设讲成已经证实的事实 |
| **研究方法** | 主角尝试验证 | 调查、实验、行动蒙太奇 | 保留关键变量和基本方法；不得发明真实研究没有的实验步骤 |
| **实验数据**（也可为访谈、观察、案例等证据） | 角色发现关键证据 | 屏幕数字、图表、证物或现场线索 | 真实数值必须准确；定性研究不能强行变成量化实验 |
| **研究结论** | 真相揭晓 | 高潮、情绪转折、澄清 | **结果决定剧情，不得反过来让剧情决定结果** |
| **研究局限** | 结尾仍存在疑问 | 新疑点、开放结局 | 不夸大研究适用范围；局限不得被删除而造成误导 |
| **未来研究** | 下一集线索 | 后续问题、新角色或新任务 | 只有原文有未来研究建议才可表述为作者提出；链接其他论文时必须有真实、可核验的文献关系，不编造续作 |

### 映射执行法
1. 先辨认是否存在该类**真实论文事实**：`SUPPORTED` / `NOT_APPLICABLE` / `UNVERIFIED`。理论/设计/访谈类论文可能没有假设、实验数字或未来研究；对应不适用即可。
2. 对每个 `SUPPORTED` 的要素记录：`academic_element`、`source_fact_ids`、`paper_source`、`drama_plot_function`、`performance_mode`、`creative_allowance`、`prohibited_distortion`、`truth_status`、`audit_status`。
3. 先看论文内容是否适合成为行动/悬念/冲突，再设计角色和表现；不可按 Introduction=第一集、Method=第二集、Results=第三集硬编码章节顺序；多个论文内容要素可共用一个戏剧节拍，一个事实也可以支撑多个节拍。
4. 对不同方案重新组合**人物视角、叙事机制与戏剧表演规则**，但对同一论文不可替换真实实验条件、结果和限定词。历史/系统/穿越等世界设定仅是虚构包装。
5. 逐集交付时再检查：表演动作是否让人理解事实？资料未支持的研究观点是否被冒充原文？数据及重要否定/概率措辞是否准确？隐藏剧透的第一轮卡片不得泄露本映射的内部细节。

## 4. 内部 Drama Blueprint 的推荐结构
每套详细蓝图在 `drama_blueprints.md` 中至少包含（按模板 `batch_id + option_id` 唯一标识）：
```yaml
batch_id: R001
option_id: A
genre: 悬疑
source_fact_ids: [F001, F004]
characters:
  count: 2
  roles:
    - identity: 虚构调查者
      goal: 验证某个真实的研究问题
      personality: 谨慎
      relationships: 与搭档互相怀疑
      truth_status: FICTIONAL_DEVICE
conflict:
  opposing_demands: [追求快速答案, 追求证据可靠]
  obstacles: [证据不足]
  escalation: [每次验证都增加新的限定]
plot:
  inciting_incident: 可表演的研究动机（虚构桥段）
  actions: [具体行动]
  surprise: 人物产生认知转折（不篡改研究结果）
  climax: 与研究证据相符的关键揭示
  outcome: 不超过研究实际结论的结果
emotion:
  emotional_beats: [好奇, 紧张, 怀疑, 释然]
performance:
  dialogue_tone: 紧张而克制
  pauses: 关键数据前停顿
  actions: [观察, 指认]
  expressions: [迟疑]
  camera: [近景, 反打]
rhythm:
  opening_hook: 开场数秒提出问题
  turning_points: [T1, T2]
  episode_cliffhangers: [尚待解决的真实问题]
research_drama_mapping:
  - academic_element: 研究背景
    source_fact_ids: [F001]
    drama_plot_function: 主角陷入困境
    performance_mode: 用具体事件开场
    truth_status: FICTIONAL_DEVICE
  - academic_element: 文献争议
    status: NOT_APPLICABLE
episode_plan: 待由论文内容密度确定
forbidden_distortions: [不改变研究统计结论]
```
上述值仅示范**字段和数据形状**，不得复制到真实论文作为已存在研究事实。

## 5. 方案选择与“换一波”更新机制
- AI 内部用上面的六类表演语法与八类映射校验 **3套真正不同**的蓝图；用户面前**每轮仅展示** A/B/C 各自的 `剧名、主题、设定、背景`。
- 允许用户直接回复“换一波”“再来三个”“都不喜欢”等表达：不用重新读取已有合格事实库，针对同一篇论文重新提出**下一批三套**，保持每批内 A/B/C 独立，批次命名 `R001, R002, ...`。
- 刷新应优先避免重复使用以前轮次的**具体标题、标签组合、叙事视角、冲突驱动机制**；不能保证每次无限创新，尤其在论文事实有限时，不可以为了新鲜而杜撰研究。
- `template_options.md` 只存当前批次四字段展示，`template_history.md` 存历次方案的批次归属；`drama_blueprints.md` 保留历次内部映射。用户默认只选最新批次 A/B/C；明确“第一波 B”则到历史记录中定位。无歧义才继续。
- 在选择卡后写“请选择 A、B 或 C；不满意可回复‘换一波’。”。不显示冲突、人物、Hook、剧情、时长等其他候选信息。
- 用户选定后才编写分集与全镜头脚本。局部调整对白无需再三选；重新选择故事方向则重新展示选择卡。

## 6. 集数、时长与双画幅
依研究节点密度、角色行动、转折合理性规划短剧总集数，每集约 45–90 秒仅作为参考，绝不固定三集或照搬 PaperTok 八镜头。竖屏9:16与横屏16:9使用相同论文事实、情节和对白，但分别安排人物与数据的镜头位置；不只改变分辨率。

## 7. 学术事实等级与演出标注
- `A_CORE`：研究问题、关键方法条件、结果、重要限定，不可改动。
- `B_COMPRESSIBLE`：次要材料可压缩，保留可定位的论文原文入口。
- `C_STAGING`：人物、对话、道具、舞台、镜头可以创造，必须标注虚构性，不能伪装成论文的被试或作者真实经历。
- 负结果、方法失败或开放结论完全可以成为合理的“澄清式”情绪高潮，但不能虚构显著反转。
