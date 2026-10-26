# PaperDrama v2.1｜输出与数据结构规范

## 默认配置
- 学术受众：**非本领域大学生**。
- 媒介：同时支持 **9:16竖屏**、**16:9横屏**短剧，单套故事和对白、逐镜双画幅说明。
- 首次选择页：**恰好3套**候选，每套**仅** `剧名、主题、设定、背景` 四个字段 + A/B/C 编号；不得泄露故事细节。
- 分类依据：`references/narrative-library.md`，28主题+42设定+11背景+2可选内容受众，共83个标签；选择页不展示“受众”分类。
- 每篇论文独立输出到 `outputs/<论文文件名>/`，不静默覆盖旧结果。

## 阶段 A：用户还没选模板
自动分析论文，保存：
- `paper_facts.md`：元数据、阅读范围、事实 ID、问题/矛盾/假设/方法/证据/结论/局限、核心限定及来源。
- `dramatic_opportunities.md`：具有证据锚点的戏剧机会，内部评分和风险。
- `drama_blueprints.md`：**内部**详细的三套叙事机制、人物关系、冲突、可能的节拍、事实映射、剧集数量与计划时长（这些细节不在选择界面展示）。
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
上面内容为**字段格式示意**，不可作为所有论文的固定方案。对话直接展示这三个选项，然后只问“请选择 A、B 或 C”。禁止添加人物、Hook、故事概况、冲突和结局、集数、每集时长、推荐理由、结果/证据说明等内容。
- `traceability_matrix.md`：内部事实→戏剧结构映射及论文页码。
- `paperdrama.json`：见下方数据协议。

阶段 A 状态为 `AWAITING_TEMPLATE_SELECTION`，`selected_template_id=null`。不得把任何方案标记为已经由用户确认；`full_script.md` 不能作为完成成果出现。

## 阶段 B：用户选择 A/B/C 后
保存：
- `series_outline.md`：剧名、所选方案、总集数、每集题目/学术目标/故事目标/计划时长及总时长。
- `full_script.md`：**全部剧集**的全部场景、镜头编号、起止秒数、机位、可表演动作、全部对白与人物情绪、配音/环境声/音效/字幕与证据 ID；每镜同时含 `vertical_9_16`、`horizontal_16_9` 两种构图（若用户明确只要一种则按需收敛）。
- `quality_report.md`：事实一致性、戏剧质量和镜头时长总和审查结果 `PASS / REVIEW / FAIL`。
- 更新 `traceability_matrix.md` 和 `paperdrama.json`，状态 `SCRIPT_READY_FOR_REVIEW` 或事实无法核实时 `BLOCKED_FOR_FACT_REVIEW`。

## paperdrama.json 样式与必需字段
```json
{
  "skill_version": "2.1.0",
  "workflow": {
    "status": "AWAITING_TEMPLATE_SELECTION",
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

阶段 B 更新 `workflow.selected_template_id`（必须是用户真正选择的 A/B/C）、`selected_by_user=true`，并填写：
- `series.title`、`series.total_episode_count`、`series.total_duration_s`、`series.episode_duration_s`。
- `series.episodes[].id/title/duration_s/academic_goal/fact_ids/scenes`。
- `series.episodes[].scenes[].id/location/duration_s/shots`。
- `shots[].id/start_s/end_s/duration_s/camera/action/dialogue_lines/subtitles/audio/fact_ids/truth_status/vertical_9_16/horizontal_16_9`。
- 如用户明确只要一种画幅，记录 `defaults.media_aspect_ratios` 的有效覆盖值并允许省略另一种画幅镜头字段。
- `full_script.md` 是主要交付，JSON 不可取代实际可读脚本。

## 验收不变量
1. 首次候选展示：恰好3套；每套仅剧名、主题、设定、背景。保存的 `template_options.md` 与对话内容一致（末尾选择提示不计）。
2. 默认受众为非本领域大学生；两种画幅同时有实质性构图建议。
3. 事实 ID 可溯源，研究结论/样本/局限不可因剧情需要被改写。
4. 全部镜头时间之和 = 场景时长；场景时长之和 = 单集时长；单集时长之和 = 全剧总时长。
5. 用户未选择前不写最终脚本；用户选择后输出所有剧集的完整对白、镜头、音效；不只输出故事梗概。
6. 未经用户实际审核，`human_approved=false`。
