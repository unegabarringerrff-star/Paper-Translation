# 交付规范

## 目录与文件
- paper_facts.md：论文元数据；阅读覆盖程度；按 motivation/method/finding/contribution 分组事实；七类戏剧标签；A/B/C 取舍；缺失信息。
- dramatic_opportunities.md：最多4项“值得传播的事实/贡献”与最多4种叙事机会。每项包含依据 fact_id、优点、歪曲风险、分数与排序。
- drama_blueprints.md：建议 1–3 套蓝图。必须说明人物目标、冲突、场景行动、情绪和节拍，以及原文的真实性边界。
- traceability_matrix.md：`beat_id | 剧情功能 | fact_ids | 页码/节 | 转译方式 | 不可更改条件 | 风险 | evidence_ui`。
- quality_report.md：两项审核 PASS/REVIEW/FAIL；缺失证据；数值核查；结论合规；仍需人确认的事项；复测摘要。
- paperdrama.json：供下一阶段调用的机器可读结构；JSON 格式必须可解析。

## JSON 参考形状（以下为字段说明，实际必须输出合法 JSON）
```json
{
  "skill_version": "1.0.0",
  "paper": {"title": "", "authors": [], "year": null, "doi": null, "source_file": "", "pages_read": [], "missing_sections": []},
  "facts": [{"fact_id":"F001", "bucket":"motivation", "tags":["research_question"], "statement":"", "source":{"page":1,"section":"", "locator":""}, "priority":"A_CORE", "certainty":"supported", "qualifiers":[]}],
  "candidate_findings": [{"id":"C01", "statement":"", "fact_ids":["F001"], "concrete_reason":"", "real_world_link":""}],
  "opportunities": [{"id":"O01", "type":"curiosity", "hook_question":"", "source_fact_ids":["F001"], "proposed_roles":[], "scores":{"fidelity":5,"dramatic_potential":3,"relevance":4,"adaptability":4}, "risk":"", "recommended":true}],
  "blueprints": [{"id":"D01", "opportunity_id":"O01", "genre":"", "audience":"", "episode_count":1, "episode_duration_range_s":[45,90], "central_question":"", "central_conflict":"", "role_archetypes":[], "beats":[{"beat_id":"B01","name":"hook","dramatic_function":"","academic_function":"","source_fact_ids":["F001"],"staging_idea":"","truth_status":"FICTIONAL_DEVICE","duration_hint_s":8,"risk":"","evidence_ui":""}], "continuity_constraints":[], "human_approved":false}],
  "checks": {"fact_review":"REVIEW", "drama_review":"REVIEW", "unverified_items":[], "blocking_issues":[]}
}
```

校验条件：每个 `source_fact_ids` 都引用存在的 fact_id；每个 `A_CORE` 有明确来源；`human_approved` 除非用户实际批准否则为 false；结论或方法不应根据戏剧需要被改写。若来源材料无页码，source.page 使用 null 并记录 section/locator，不编造页码。
