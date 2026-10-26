# PaperDrama v2.0 输出与数据结构规范

## 阶段、状态与文件
每篇论文有独立输出目录 `outputs/<论文文件名>/`。

**阶段 A｜展示模板等待选择**
- `paper_facts.md`：论文元数据、文本覆盖情况、学术事实库（四大桶 + 不限于七个叙事标签）、关键限定、原文依据。
- `dramatic_opportunities.md`：最多四项传播/戏剧化机会及可信度与表演可行性。
- `drama_blueprints.md`：各候选研究知识点 → 戏剧功能/叙事节拍/表演规则的映射。
- `template_options.md`：**恰好3套**各有 distinct story mechanics 的选项 A/B/C，用户可选，必须实际在对话展示，不能仅保存在文件。
- `traceability_matrix.md`：`template/beat | academic_claim | fact_id | PDF页码/节 | literal/analogy/fictional | 约束与风险`。
- `paperdrama.json`：已完成阶段A的数据，`workflow.status=AWAITING_TEMPLATE_SELECTION`，`selected_template_id=null`，不得出现已完成的最终剧本。
- 此时**不应**输出 `full_script.md` 作为完成作品。

**阶段 B｜用户已确认选项后**
- `series_outline.md`：最终片名、所选模板、角色设定、总集数、每集学术与剧情目标、每集时长（mm:ss）、总时长、拆集依据。
- `full_script.md`：**主要交付物**；全部剧集、每场及每镜的时间码/景别/动作/完整对白或明确静默/情绪/BGM/SFX/字幕/学术原文线索与虚构声明。
- `quality_report.md`：事实与戏剧质量与制作核验，列出各项 PASS/REVIEW/FAIL、修改记录、需人核验项、总时长验算。
- 更新 `traceability_matrix.md`：新增 `episode/scene/shot | claim | fact_id | 页码和图表 | 虚构性 | 核验`。
- 更新 `paperdrama.json`：`workflow.status=SCRIPT_READY_FOR_REVIEW` 或 `BLOCKED_FOR_FACT_REVIEW`；`selected_template_id` 必须是实际已确认 A/B/C。
- `full_script.json` 为可选结构化镜头表，脚本正文不可缺。

## paperdrama.json 最小结构（合法 JSON 示例）
```json
{
  "skill_version": "2.0.0",
  "workflow": {
    "status": "AWAITING_TEMPLATE_SELECTION",
    "template_options_presented": true,
    "selected_template_id": null,
    "selected_by_user": false,
    "human_approved": false
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
      "statement": "示例学术事实",
      "source": {"pdf_page": 1, "printed_page": null, "section": "Introduction", "locator": "第一段"},
      "priority": "A_CORE",
      "certainty": "supported",
      "qualifiers": []
    }
  ],
  "opportunities": [
    {"id": "O01", "type": "curiosity", "source_fact_ids": ["F001"], "risks": []}
  ],
  "template_options": [
    {
      "id": "A",
      "genre": "调查悬疑",
      "title": "候选标题A",
      "hook": "一个真实研究问题引发的悬念",
      "characters": [],
      "dramatic_mechanism": "以调查推进证据",
      "beats": [],
      "episode_count_estimate": 1,
      "episode_durations_estimate_s": [70],
      "source_fact_ids": ["F001"],
      "fiction_disclaimer": "人物桥段为虚构"
    },
    {
      "id": "B",
      "genre": "伦理困境",
      "title": "候选标题B",
      "hook": "",
      "characters": [],
      "dramatic_mechanism": "人物决策和代价",
      "beats": [],
      "episode_count_estimate": 1,
      "episode_durations_estimate_s": [85],
      "source_fact_ids": ["F001"],
      "fiction_disclaimer": "人物桥段为虚构"
    },
    {
      "id": "C",
      "genre": "荒诞隐喻",
      "title": "候选标题C",
      "hook": "",
      "characters": [],
      "dramatic_mechanism": "拟人和寓言",
      "beats": [],
      "episode_count_estimate": 2,
      "episode_durations_estimate_s": [60, 60],
      "source_fact_ids": ["F001"],
      "fiction_disclaimer": "人物桥段为虚构"
    }
  ],
  "series": null,
  "checks": {
    "facts": "REVIEW",
    "narrative": "REVIEW",
    "production": "REVIEW",
    "blocking_issues": []
  }
}
```

**阶段 B 更新示意**：将 `workflow.selected_template_id` 写为用户选择的 `A|B|C`，`selected_by_user=true`，`status=SCRIPT_READY_FOR_REVIEW`（若不满足事实约束则 `BLOCKED_FOR_FACT_REVIEW`）；`series` 应包含：
- `title`、`total_episode_count`、`total_duration_s`、`episode_duration_s` 数组、`selection_rationale`
- `episodes[].id/title/duration_s/academic_goal/fact_ids/scenes`
- `scenes[].id/location/duration_s/shots`
- `shots[].id/start_s/end_s/duration_s/camera/action/dialogue_lines/subtitles/audio/fact_ids/truth_status`
- 每条 `dialogue_lines[]` 至少标识角色与完整台词（或注明无对白）。
- 完整脚本仍必须以 `full_script.md` 交付；数据结构不能取代人能阅读的分镜脚本。

## 校验
1. 正式进入阶段B前必须已在对话展示 A/B/C 三方案并收到选择；阶段A不得暗设 `selected_template_id` 或标记 `selected_by_user=true`。
2. 全部 `source_fact_ids` 必须引用已有的 fact_id；`A_CORE` 需可定位来源；找不到证据的事实不能写成真实结论。
3. 每一镜头时间和场景/剧集时长按整数秒保存：`end_s-start_s=duration_s`。逐层检查 `Σshots=scene`、`Σscenes=episode`、`Σepisode=series`。
4. `full_script.md` 必须涵盖全部剧集的完整对白、表演动作、镜头、音效、场景、字幕和事实锚点；不能只给分集大纲、台词样例或首集。
5. 不得因剧本变好看而虚构实验结果、统计显著性、研究者自述或真实被试行为。
6. 未经人类实际最终审核，`human_approved=false`。
