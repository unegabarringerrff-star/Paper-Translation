# PaperDrama v3.1｜五档强度及完整剧本验收

这些是应执行的测试，不是已经完成的Codex真实运行记录。用 assets/demo-input.md 的虚构论文与真实可读PDF分别测试。

## T01 一次输入直接成稿（主要通过条件）
输入PDF + 主题“悬疑”、设定“系统”、背景“校园”，调用Skill。**通过**：不中途生成A/B/C、不出现“换一波/请选择风格/下一步继续吗”；同轮保存 full_script.md、series_outline.md、paper_facts.md、dramatic_opportunities.md、drama_blueprint.md、beat_sheet.md、quality_report.md、content_tradeoff_report.md、traceability_matrix.md、paperdrama.json。

## T02 自然语言混合输入
输入“把PDF改成古代宫斗戏，主角穿越，发生在宫廷；其他你决定”。通过：识别主题宫斗/设定穿越/背景宫廷，无中途确认；自主规划集数和镜头。

## T03 首轮输入不完整
仅给PDF但未提供三维度。通过：只一次合并问缺失项，不依次追问；当用户补充后直接完成，不给中间推荐。若用户说“自由发挥”则不用再问。

## T04 剧情极度夸张仍守研究事实
虚构论文24名参与者、两组各12人、组间差异未显著；用户指定戏剧强度5并希望结尾大胜利。通过：戏剧中可有背叛、激烈冲突、虚构世界的胜负，但**论文结果仍不显著**，数据未修改，核心断言有fact_id，声明 FICTIONAL_DEVICE。

## T05 强度对应的开场与镜头
**4–5级**检查前3–5秒是否有可视行动或强钩子；**1–2级**允许稳镜头、论文证据解释和自然对话，不应以缺少危险事件判失败。各级镜头仍要服务信息或情绪，9:16/16:9与景别、动作、声音等说明可执行。

## T06 档位对应的戏剧强度
1级以研究理解推进即可，不强制对抗或反转；2级轻冲突；3级需要角色目标和可信的因果变化；4–5级须有明显的代价、逆转、情绪反差和符合设定的悬念。不得仅靠感叹号或镜头效果计数合格。

## T07 影片形式双画幅
默认9:16与16:9分别给具体构图、字幕位置和空间安排；不能简单写“同上”；用户指定横屏时仅输出16:9。

## T08 完整交付与总时长
每集/每场/每镜时间码、全部台词/明确静默、音效、切换、字幕、研究事实ID或 FICTIONAL_DEVICE 都齐全。镜头时间和=场景、场景=单集、所有集=总时长。不得只输出剧本梗概、第一集样例或空白占位符。

## T09 学术领域兼容
分别输入实验、定性、理论、设计研究。通过：映射不适用内容写 NOT_APPLICABLE；不凭空编造访谈/量化指标/文献争议；使用论文真实核心问题搭建虚构冲突。

## T10 存档与输出状态
paperdrama.json是合法JSON、workflow.status=SCRIPT_READY_FOR_REVIEW或BLOCKED_FOR_FACT_REVIEW，user_intermediate_approval_required=false；无 selected_template_id、generation_round、template_options、template_history、AWAITING_TEMPLATE_SELECTION。输出声明AI创作不等于人类审稿。

## T11 失败样本与自动重写
找一个剧情平淡、长篇论文朗读、镜头同质化的初稿，运行内部启发式评分。通过：**仅4–5级**以关键戏剧张力评分低于4分触发重写；1–2级以学术内容覆盖、清晰度及恰当表演为验收重点；所有档位记录修订理由和自评分，不伪装为外部效果验证。

## T12 不可读取PDF
若扫描件不能识别/文件损坏：须注明阻塞，不能编出论文发现。可读取部分只能在受支持范围内转译并标明缺口。

## T13 文件与规则静态一致性
SKILL、README、output-schema、script-writing、drama-blueprint、cinematic-tension、tests不得仍要求三套候选、A/B/C选择或刷新流程；唯一的相关词汇只允许用于说明**已被取消**的旧流程。版本号统一3.1.0，且要引用 references/dramatic-intensity.md；不能把1–2级也要求高强度冷开场。

## T14 五档输入解析
同一 PDF+主题/设定/背景分别输入“戏剧强度：1、2、3、4、5”，并测试不填写（默认4）。
**通过**：input_config.dramatic_intensity 和 intensity.level 均为同一整数，档名准确，默认4；不会中途要求用户再次选档。越界输入需说明归一化边界。

## T15 相同论文五档内容取舍必须明显不同
用同一论文、同一主题/设定/背景输出五档并检查两个报告。
**通过**：1级较完整讲明关键研究方法、证据、结论、局限；2级压缩综述，轻度剧情；3级保留必要方法限定、核心证据并让研究推动故事；4级正片聚焦1–2项关键发现，将次要学术内容转到事实卡/附录；5级高度架空但至少一个真实研究问题或发现与限定就近可见。不能五级只在台词口气和镜头数上有所不同。

## T16 六种去向与逐事实覆盖
验证 content_tradeoff_report.md 和 paperdrama.json.content_tradeoffs。
**通过**：每个可靠 fact_id 有去向（ON_SCREEN_EXPLICIT / ON_SCREEN_SIMPLIFIED / FACT_CARD / APPENDIX_ONLY / OMITTED_NONESSENTIAL / FICTIONAL_ANALOGY），定位清晰、理由和潜在误解说明完整。研究完整事实库不因强度变化而删除。

## T17 高强度“替换”不篡改科研结论
采用 assets/demo-input.md：24人，两组各12，主观完成感均值有差异但**未达显著性**。
**通过**：4级可引入虚构校园危机，5级可引入虚构魔法战争；真实实验与“不显著”不被说成显著，片中研究断言带限定；虚构世界事件标 FICTIONAL_DEVICE。

## T18 低强度不强制高张力
以强度1、2分别运行。
**通过**：没有必须3–5秒爆炸/背叛/倒计时的规则，允许镜头克制与研究方法解释；生成完整可拍的短剧而不是纯学术报告，也不能被4级的戏剧性评分判失败。

## T19 切换档位需要实质改编
先生成强度5，然后只说“改为强度2”；再从2改为4。
**通过**：直接复用学术事实库，不重新索取PDF/题材/设定；在脚本中实质调整方法与证据的呈现位置、冲突等级、镜头与情绪，不是替换标题或等级文字；更新内容取舍清单与 JSON。

## T20 实证真假跨档一致
同一论文五档逐个抽查样本、数值、方法性质、显著性、效应方向、局限和假设状态。
**通过**：关键科学真值不随等级改变。5级也不可把相关写成因果、虚构的敌我冲突写成作者亲身经历；如果没有统计数据、未来研究计划则必须标 NOT_APPLICABLE。

## T21 JSON 元数据与溯源可复核
解析 paperdrama.json。
**通过**：skill_version=3.1.0；intensity.level 是1–5整数，与 input_config.dramatic_intensity 一致；intensity.coverage 内的 fact_id 均能在 facts 找到；content_tradeoffs 的 fact_id 都存在；human_approved 未经真实批准保持 false。
