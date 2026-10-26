# PaperDrama v2.2｜输出与数据结构规范

## 默认配置
- 学术受众：**非本领域大学生**。
- 媒介：同时支持 **9:16竖屏**、**16:9横屏**短剧，单套故事和对白、逐镜双画幅说明。
- 首次与每次“换一波”后的选择页：**恰好3套当前批次候选**，每套**仅** `剧名、主题、设定、背景` 四个字段 + A/B/C 编号；不得泄露故事细节。选择页尾句为“请选择 A、B 或 C；不满意可回复‘换一波’。”。
- 分类依据：`references/narrative-library.md`，28主题+42设定+11背景+2可选内容受众，共83个标签；选择页不展示“受众”分类。
- 每篇论文独立输出到 `outputs/<论文文件名>/`，不静默覆盖旧结果。

## 阶段 A：用户还没选模板
自动分析论文，保存：
- `paper_facts.md`：元数据、阅读范围、事实 ID、问题/矛盾/假设/方法/证据/结论/局限、核心限定及来源。
- `dramatic_opportunities.md`：具有证据锚点的戏剧机会，内部评分和风险。
- `drama_blueprints.md`：**内部**详细蓝图，须包含六项 Drama 语法对象：`characters`（count, identity, goal, personality, relationships）、`conflict`（opposing_demands, obstacles, escalation）、`plot`（inciting_incident, actions, surprise, climax, outcome）、`emotion.emotional_beats`、`performance`（dialogue_tone, pauses, actions, expressions, camera）、`rhythm`（opening_hook, turning_points, episode_cliffhangers）。另含八项论文→Drama 转译的状态、事实ID、表演方式与不得失真的边界。每套内部详情须以 `batch_id + option_id` 唯一索引，防止换一波之后错配。
- `template_options.md`：对外可展示的**极简候选卡**，每套仅 `id、title、themes、settings、background`：
```text
A｜《有戏剧张力的剧名》
主题：悬疑、科幻
设定：系统
背景：校园

B｜《另一个有戏剧张力的剧名》
主题：喜剧、脑洞
设定：灵魂互换
背景：职场

C｜《第三个有戏剧张力的剧名》
主题：权谋
设定：强强联合
背景：架空
```
上面内容为**字段格式示意**，不可作为所有论文的固定方案。对话仅展示**最新一轮**的三个选项，然后写“请选择 A、B 或 C；不满意可回复‘换一波’。”。不增加第五个候选内容字段。禁止添加人物、Hook、故事概况、冲突和结局、集数、每集时长、推荐理由、结果/证据说明等内容。
- `template_history.md`：**内部**历轮批次的 A/B/C 选项及所对应的 Blueprint ID，保存 `batch_id`、`generation_round`、剧名、标签、叙事机制摘要和是否已选等。既有内容不静默丢弃，**不在选择页展示历次内容**。
- `traceability_matrix.md`：内部事实→戏剧结构映射及论文页码；八类映射逐项标记 `SUPPORTED / NOT_APPLICABLE / UNVERIFIED`，每个已采用的学术要素带 `source_fact_ids`、`performance_mode`、`prohibited_distortion`、`audit_status`。
- `paperdrama.json`：见下方数据协议。

阶段 A 状态为 `AWAITING_TEMPLATE_SELECTION`，`selected_template_id=null`、`selected_batch_id=null`。用户说“换一波”时不再重新构建已校验的事实库，直接将 `generation_round` 加一、`active_batch_id` 从 R001 变为 R002/R003…，将旧当前三选项存入 `template_history.md` 并以新选项替换 `template_options.md`。允许连续多轮；优先生成与当前和历史方案有实际区别的叙事，不通过编造研究提升新颖度。刷新不会把 `selected_by_user` 改为 true，也不会创建完整脚本。

## 阶段 B：用户选择 A/B/C 后
保存：
- `series_outline.md`：剧名、所选方案、总集数、每集题目/学术目标/故事目标/计划时长及总时长。
- `full_script.md`：**全部剧集**的全部场景、镜头编号、起止秒数、机位、可表演动作、全部对白与人物情绪、配音/环境声/音效/字幕与证据 ID；每镜同时含 `vertical_9_16`、`horizontal_16_9` 两种构图（若用户明确只要一种则按需收敛）。
- `quality_report.md`：事实一致性、戏剧质量和镜头时长总和审查结果 `PASS / REVIEW / FAIL`。
- 更新 `traceability_matrix.md` 和 `paperdrama.json`，状态 `SCRIPT_READY_FOR_REVIEW` 或事实无法核实时 `BLOCKED_FOR_FACT_REVIEW`。

## paperdrama.json 样式与必需字段
```json
{
  "skill_version": "2.2.0",
  "workflow": {
    "status": "AWAITING_TEMPLATE_SELECTION",
    "generation_round": 1,
    "active_batch_id": "R001",
    "selected_batch_id": null,
    "selected_template_id": null,
    "selected_by_user": false,
    "human_approved": false
  },
  "defaults": {
    "academic_audience": "非本领域大学生",
    "media_aspect_ratios": ["9:16", "16:9"],
    "language": "zh-CN"
  },
  "paper": {
    "title": "",
    "source_file": "paper.pdf",
    "pages_read": [],
    "missing_sections": []
  },
  "facts": [
    {
      "fact_id": "F001",
      "bucket": "motivation",
      "tags": ["research_question"],
      "statement": "示例事实（执行时必须替换成原文真实内容）",
      "source": {"pdf_page": 1, "section": "Introduction", "locator": "第一段"},
      "priority": "A_CORE",
      "certainty": "supported",
      "qualifiers": []
    }
  ],
  "opportunities": [
    {"id": "O01", "type": "curiosity", "source_fact_ids": ["F001"], "risks": []}
  ],
  "template_options": [
    {"id": "A", "title": "剧名A", "themes": ["悬疑"], "settings": ["系统"], "background": ["校园"]},
    {"id": "B", "title": "剧名B", "themes": ["喜剧"], "settings": ["灵魂互换"], "background": ["职场"]},
    {"id": "C", "title": "剧名C", "themes": ["权谋"], "settings": ["强强联合"], "background": ["架空"]}
  ],
  "internal_blueprints_file": "drama_blueprints.md",
  "template_history_file": "template_history.md",
  "academic_to_drama_map_file": "traceability_matrix.md",
  "series": null,
  "checks": {
    "facts": "REVIEW",
    "narrative": "REVIEW",
    "production": "REVIEW",
    "blocking_issues": []
  }
}
```

**注意**：JSON 示例表示字段形状，不是实际论文的事实或固定类型。真正输出必须按论文生成三个叙事机制不同的方案；对外 `template_options` 对象只能保留 5 个属性（含 id），不得包含 `hook`、`characters`、`beats`、`episode_count_estimate`、`plot` 等剧情或制作信息。

阶段 B 更新 `workflow.selected_batch_id`（默认最新的 `active_batch_id`，但可根据用户明确请求选择历史批次）、`workflow.selected_template_id`（该批次的 A/B/C）、`selected_by_user=true`，**用 `selected_batch_id+selected_template_id` 精准定位内部蓝图**，并填写：
- `series.title`、`series.total_episode_count`、`series.total_duration_s`、`series.episode_duration_s`。
- `series.episodes[].id/title/duration_s/academic_goal/fact_ids/scenes`。
- `series.episodes[].scenes[].id/location/duration_s/shots`。
- `shots[].id/start_s/end_s/duration_s/camera/action/dialogue_lines/subtitles/audio/fact_ids/truth_status/vertical_9_16/horizontal_16_9`。
- 如用户明确只要一种画幅，记录 `defaults.media_aspect_ratios` 的有效覆盖值并允许省略另一种画幅镜头字段。
- `full_script.md` 是主要交付，JSON 不可取代实际可读脚本。

## 验收不变量
1. 首次及每次刷新候选展示：恰好3套**当前批次**；每套仅剧名、主题、设定、背景。保存的 `template_options.md` 与当轮对话一致（末尾选择/刷新提示不计）。旧批次保存在内部 `template_history.md`。
2. 用户“换一波”可连续执行、不需理由、不重复处理同一论文事实；`generation_round` 自增、批次ID唯一、A/B/C 始终只指向最新一批。选历史方案需要明确旧轮次和选项；如果参照不清楚须先确认轮次。
3. 默认受众为非本领域大学生；两种画幅同时有实质性构图建议。
4. 内部蓝图必须填写六类 Drama 表演语法和八类论文映射，不可留空凑形式。每条有研究断言的映射须有 `fact_id`；不适用的研究元素标记 `NOT_APPLICABLE`，不能凭空发明实验/争议/未来计划。研究结论、样本与局限不得因剧情修改。
5. 全部镜头时间之和 = 场景时长；场景时长之和 = 单集时长；单集时长之和 = 全剧总时长。
6. 用户未选择前不写最终脚本；用户选择后输出所有剧集的完整对白、镜头、音效；不只输出故事梗概。
7. 未经用户实际审核，`human_approved=false`。
