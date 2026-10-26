# PaperDrama v3.0｜人工复测与静态验收

这些是应执行的测试，不是已经完成的Codex真实运行记录。用 assets/demo-input.md 的虚构论文与真实可读PDF分别测试。

## T01 一次输入直接成稿（主要通过条件）
输入PDF + 主题“悬疑”、设定“系统”、背景“校园”，调用Skill。**通过**：不中途生成A/B/C、不出现“换一波/请选择风格/下一步继续吗”；同轮保存 full_script.md、series_outline.md、paper_facts.md、dramatic_opportunities.md、drama_blueprint.md、beat_sheet.md、quality_report.md、traceability_matrix.md、paperdrama.json。

## T02 自然语言混合输入
输入“把PDF改成古代宫斗戏，主角穿越，发生在宫廷；其他你决定”。通过：识别主题宫斗/设定穿越/背景宫廷，无中途确认；自主规划集数和镜头。

## T03 首轮输入不完整
仅给PDF但未提供三维度。通过：只一次合并问缺失项，不依次追问；当用户补充后直接完成，不给中间推荐。若用户说“自由发挥”则不用再问。

## T04 剧情极度夸张仍守研究事实
虚构论文24名参与者、两组各12人、组间差异未显著；用户指定戏剧强度5并希望结尾大胜利。通过：戏剧中可有背叛、激烈冲突、虚构世界的胜负，但**论文结果仍不显著**，数据未修改，核心断言有fact_id，声明 FICTIONAL_DEVICE。

## T05 电影化开场与镜头动机
检查每集前3–5秒是否具有可视行动或悬念，而非论文旁白；镜头有景别、机位/运镜、前中后景、人物走位、动作、表情/停顿、转场与音效，镜头语言必须服务情节。若开场在纯理论文献下无法如此处理，应给出清晰创造性视觉隐喻。

## T06 因果升级与情绪对比
每集至少一项局势真正变化；每场具人物目标、对抗、障碍、行动、反行动及代价；高低情绪交替，集尾悬念有具体下一问题。不得仅靠吵架或惊叹词计数合格。

## T07 影片形式双画幅
默认9:16与16:9分别给具体构图、字幕位置和空间安排；不能简单写“同上”；用户指定横屏时仅输出16:9。

## T08 完整交付与总时长
每集/每场/每镜时间码、全部台词/明确静默、音效、切换、字幕、研究事实ID或 FICTIONAL_DEVICE 都齐全。镜头时间和=场景、场景=单集、所有集=总时长。不得只输出剧本梗概、第一集样例或空白占位符。

## T09 学术领域兼容
分别输入实验、定性、理论、设计研究。通过：映射不适用内容写 NOT_APPLICABLE；不凭空编造访谈/量化指标/文献争议；使用论文真实核心问题搭建虚构冲突。

## T10 存档与输出状态
paperdrama.json是合法JSON、workflow.status=SCRIPT_READY_FOR_REVIEW或BLOCKED_FOR_FACT_REVIEW，user_intermediate_approval_required=false；无 selected_template_id、generation_round、template_options、template_history、AWAITING_TEMPLATE_SELECTION。输出声明AI创作不等于人类审稿。

## T11 失败样本与自动重写
找一个剧情平淡、长篇论文朗读、镜头同质化的初稿，运行内部启发式评分。通过：低于4分的关键项重写；记录理由和新得分，不把自评分伪装为外部效果验证。

## T12 不可读取PDF
若扫描件不能识别/文件损坏：须注明阻塞，不能编出论文发现。可读取部分只能在受支持范围内转译并标明缺口。

## T13 文件与规则静态一致性
SKILL、README、output-schema、script-writing、drama-blueprint、cinematic-tension、tests不得仍要求三套候选、A/B/C选择或刷新流程；唯一的相关词汇只允许用于说明**已被取消**的旧流程。版本号统一3.0.0。
