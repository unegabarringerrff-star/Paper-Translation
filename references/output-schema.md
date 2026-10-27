# PaperDrama v3.1｜五档强度的一次输入、完整剧本输出合同

## 流程
输入：学术PDF + 用户首次给定 themes/settings/background（自然语言可用）；其他如时长/角色/**戏剧强度1–5（默认4）**/画幅可选。强度控制论文信息在正片、事实卡、附录和虚构隐喻中的去向，严格执行 `references/dramatic-intensity.md`。用户要求“自由发挥”可让 AI 补全缺项；缺少必需创作维度且未授权补全时最多一次合并询问。输入齐备后直接生成脚本，无候选方案/用户确认阶段。
状态：PROCESSING → SCRIPT_READY_FOR_REVIEW；关键事实无法核实则 BLOCKED_FOR_FACT_REVIEW。**禁止 AWAITING_TEMPLATE_SELECTION、selected_template_id、generation_round、template_options、template_history 等旧版字段/交付。**

## 文件
- full_script.md **主要交付**：全剧总集数/每集准确计划时长/总时长、全部集/场/镜与完整对白、戏剧动作、剪辑方式、音效、两画幅。
- series_outline.md：每集题名、研究锚点、戏剧目标、局势改变与时长。
- paper_facts.md：可溯源事实与源PDF位置、学术约束。
- dramatic_opportunities.md：1–4个关键戏剧锚点，内部用途。
- **content_tradeoff_report.md：逐条 fact_id 说明该强度下保留、压缩、事实卡、附录、正片省略或虚构隐喻的方式和理由；记录必要限定与潜在误解。**
- drama_blueprint.md：一套由用户首轮世界设定驱动的详细六类表演语法。
- beat_sheet.md：各集戏剧节拍、目标、障碍、升级、情绪、镜头策略。
- traceability_matrix.md：ep/scene/shot→fact_id或FICTIONAL_DEVICE、学术判定与风险。
- quality_report.md：研究底线、**强度档位一致性与内容保留审查**、张力、镜头和时间一致性自检、修订记录。
- paperdrama.json：机器可读配置、集数/时长/镜头、校验、来源。
所有文件保存 outputs/<论文文件名>/（已有文件不静默覆盖）。资料不足时报告缺失，不能填不存在的研究事实。

## paperdrama.json 最小形状（以下为字段结构示例）
```json
{
  "skill_version": "3.1.0",
  "workflow": {
    "status": "SCRIPT_READY_FOR_REVIEW",
    "user_intermediate_approval_required": false,
    "human_approved": false
  },
  "input_config": {
    "themes": [
      "悬疑"
    ],
    "settings": [
      "重生"
    ],
    "background": [
      "校园"
    ],
    "audience": "非本领域大学生",
    "dramatic_intensity": 4,
    "aspect_ratios": [
      "9:16",
      "16:9"
    ],
    "inferred_fields": []
  },
  "paper": {
    "title": "例子（应替换）",
    "source_file": "paper.pdf",
    "pages_read": [
      1
    ],
    "missing_sections": []
  },
  "facts": [
    {
      "fact_id": "F001",
      "statement": "示意事实（应替换为原文）",
      "source": {
        "page": 1,
        "section": "Introduction"
      },
      "priority": "CORE_FACT",
      "certainty": "supported"
    }
  ],
  "drama_blueprint": {
    "characters": {},
    "conflict": {},
    "plot": {},
    "emotion": {},
    "performance": {},
    "rhythm": {}
  },
  "series": {
    "title": "示意剧名",
    "total_episode_count": 1,
    "total_duration_s": 70,
    "episodes": [
      {
        "id": "EP01",
        "title": "示意集名",
        "duration_s": 70,
        "academic_anchor_ids": [
          "F001"
        ],
        "scenes": [
          {
            "id": "S01",
            "duration_s": 70,
            "shots": [
              {
                "id": "SH01",
                "start_s": 0,
                "end_s": 70,
                "duration_s": 70,
                "camera": "镜头语法需按真正作品改写",
                "action": "示意动作",
                "dialogue": [
                  "角色A：示例对白"
                ],
                "audio": "示意音效",
                "transition": "cut",
                "truth_status": "FICTIONAL_DEVICE",
                "fact_ids": [],
                "vertical_9_16": "竖屏构图说明",
                "horizontal_16_9": "横屏构图说明"
              }
            ]
          }
        ]
      }
    ]
  },
  "checks": {
    "academic_integrity": "REVIEW",
    "dramatic_tension": "REVIEW",
    "cinematic_expression": "REVIEW",
    "timing": "PASS",
    "blocking_issues": [],
    "intensity_compliance": "REVIEW",
    "content_tradeoff_integrity": "REVIEW"
  },
  "intensity": {
    "level": 4,
    "label": "强冲突短剧型",
    "policy_reference": "references/dramatic-intensity.md",
    "retention_policy": "突出研究问题、1–2项核心研究证据和结果，方法细节可转至屏内来源卡或附录",
    "coverage": {
      "on_screen_fact_ids": [
        "F001"
      ],
      "fact_card_ids": [],
      "appendix_fact_ids": [],
      "fictional_analogy_ids": [],
      "necessary_qualifiers": []
    },
    "source_facts_preserved": true
  },
  "content_tradeoffs": [
    {
      "fact_id": "F001",
      "academic_element": "research_question",
      "disposition": "ON_SCREEN_EXPLICIT",
      "onscreen_location": "EP01/S01/SH01",
      "reason": "核心研究问题必须进入正片",
      "risk": "none",
      "mitigation": "show source"
    }
  ]
}
```

注：该 JSON 例子是字段形状、不是合格的完整剧本范例；“一个70秒长镜头”等示意不得成为默认输出。实际生成必须形成有节奏变化的镜头序列与完整对白。
必须满足：`input_config.dramatic_intensity` 是1–5的整数且与 `intensity.level` 一致；按照该档完整执行论文信息保留/移动/虚构替代策略；每个提取出的事实在 `content_tradeoffs` 中有明确去向；`content_tradeoff_report.md` 的决定与 JSON 一致；高档不能修改或隐藏误导性结论。每项真实学术断言关联 fact_id 与 source；每段 FICTIONAL_DEVICE 不伪装成论文实测；shot时长逐级相加正确；每镜头默认有9:16与16:9构图；human_approved 不能凭空变 true。


## 戏剧强度 JSON 校验规则
1. intensity.level 和 input_config.dramatic_intensity 必须是相同的 1–5 整数；缺省4，用户可明确覆盖。intensity.label 必须对应五个正式名称：学术还原型、轻度剧情型、证据驱动戏剧型、强冲突短剧型、极致娱乐架空型。
2. intensity.source_facts_preserved=true 代表事实库保留全部可读取范围的论文事实，不代表视频必须播出全部事实。
3. content_tradeoffs[] 中每个事实至少一个去向，枚举为 ON_SCREEN_EXPLICIT / ON_SCREEN_SIMPLIFIED / FACT_CARD / APPENDIX_ONLY / OMITTED_NONESSENTIAL / FICTIONAL_ANALOGY。FICTIONAL_ANALOGY 是叙事形式转换，不是科学结论替换。
4. intensity.coverage.on_screen_fact_ids、fact_card_ids、appendix_fact_ids、fictional_analogy_ids 必须引用 facts 中已有的 fact_id；必要限定要在有关学术断言附近展示。
5. 1级应覆盖必要研究问题、方法、证据、结论与局限；4级应覆盖研究问题及1–2项关键发现和其范围；5级至少一个真实研究知识锚点与限定在正片可见。原文没有的字段不用强行补齐。
6. 若用户修改档位，保留 input_config 中其他创作条件，复用学术事实库，重算内容去向、故事、场景、镜头、时长与核验，更新两个报告。
7. 选择强度1–2时，不要求 4–5级的强冲突/反转评分门槛；质量指标应针对档位，而不是统一逼所有作品狗血化。
