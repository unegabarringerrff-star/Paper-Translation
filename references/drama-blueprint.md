# Drama Blueprint v3.0｜从论文事实到夸张短剧

## 先接受用户给定的世界
首次输入的 **主题、设定、背景** 是唯一创作方向，不是让AI再生成三组选项。优先用户原话；标签库仅帮助解释用户用词，不抢替用户偏好。若其设定与研究现实相差很大，可通过拟人、隐喻、奇幻场景转译，不能伪称真实研究发生在古代/荒岛/末日等空间。

## 六类媒介表演语法（唯一蓝图必须具体填写）
| 要素 | 结构化字段 | 设计重点 |
|---|---|---|
| 人物 | count, identity, goal, personality, relationships, vulnerability, secret | 角色有明确欲望、软肋、关系和改变 |
| 冲突 | opposing_demands, obstacles, escalation, irreversible_choice | 逐级升级、有对抗和真正代价 |
| 情节 | inciting_incident, actions, surprise, climax, outcome, consequence | 角色决定引发下一行动，而非随机强转折 |
| 情绪 | emotional_beats, contrast, release | 好奇/紧张/怀疑/惊讶/释然不需逐项凑齐 |
| 表演 | dialogue_tone, pauses, actions, expressions, camera, blocking | 对白有潜台词，动作和镜头推进信息 |
| 节奏 | opening_hook, turning_points, episode_cliffhangers, silence_beats | 前3–5秒视觉钩子、高潮前后反差、集尾悬念 |

按用户剧种决定何种冲突合理。科幻/宫斗/悬疑/爱情均允许极大叙事想象，但论文研究结论与虚构人物冲突必须区隔。内部 Blueprint 只有**一份已选世界观**，没有 A/B/C、generation_round 或等待选择状态。

## 八类论文→Drama映射（按实际有无选用）
| 学术单元 | 可转成的戏剧事件 | 表演方式与界限 |
|---|---|---|
| 研究背景 | 主角陷入困境 | 具体场景开局；场景可虚构，学术问题不能伪造 |
| 文献争议 | 代理角色出现立场对立 | 争论/对峙；论文无争议时虚构对抗只可用作概念隐喻 |
| 研究假设 | 人物提出赌注或挑战 | 宣言/行动；假设不是结果 |
| 研究方法 | 调查与行动 | 蒙太奇/可视化线索；若假造实验桥段须显式虚构，不能称真实过程 |
| 实验数据/定性证据 | 关键证物 | 数字原样准确；定性结论不变成量化数据 |
| 研究结论 | 真相或认识揭晓 | 可使人物处境剧变，但不能反向修改原文结果 |
| 研究局限 | 限制或余波 | 夸张人物反应可行；别消除核心适用边界 |
| 未来研究 | 续集悬念 | 可以虚构角色下一行动；不能谎称论文作者提出未写过的下一研究 |

每个真实学术主张必须关联fact_ids、论文位置和重要限定。原文没有的研究元素用 NOT_APPLICABLE。允许把不宜上屏的次要信息压缩或删除。每个场景优先有 action/counteraction 而不是单纯按 Introduction/Methods/Results 分幕。

## 生成顺序
用户主题/设定/背景 → 一个世界规则 → 一组角色与冲突 → 选取1–4个核心研究锚点 → 情节因果链 → 剧集与镜头。先通过 sources_check，然后进入 cinematic_tension 结构审查。无中途选择与模板预览。
