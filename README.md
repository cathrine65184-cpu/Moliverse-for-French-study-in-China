# Moliverse-for-French-study-in-China
A text-based adventure game for children that uses AI to introduce basic languages. It integrates word games, attribute testing, language learning, and humanities education, allowing children to naturally acquire foreign languages ​​through cross-cultural travel.
✨ 这是什么
MoliVerse 是一个面向少儿的 AI 互动叙事（Interactive Fiction）引擎 + 内容游戏。玩家化身小主人「雯雯」，陪伴法国小客人 Emilie 游历上海广东等城市，在一段段剧情中通过对话、解谜与文化碰撞学习法语（及后续更多语种）。
核心灵感来自《极乐迪斯科》（Disco Elysium）的「技能检定 + 心理拟人化旁白」叙事，但全面少儿化、零付费、无攀比、正向无惩罚，并由家长端可控。
剧情不是手写死的——而是由大语言模型实时生成，再经一套规则智能体严格校验后落地，做到「千人千面」的个性化养成体验。
🎮 核心玩法

开局性格匹配：通过童趣化的图片二选一测试（少儿简化版 MBTI），自动匹配三大人格原型之一，终身绑定。

🔥 破局者 The Ice-Breaker — 高勇气，敢开口，社交口语型
🧠 解谜家 The Decoder — 高逻辑，找规律，推理学霸型
💖 倾听者 The Empath — 高同理心，重共情，文化礼仪型


三岔路检定：每个场景固定三个选项——A 保守推进 / B 技能检定 / C 文化碰撞。检定难度受玩家当前词汇等级约束。
属性拟人化旁白：「你的【逻辑】小人在疯狂警告你……」式心理独白，赋予剧本灵魂。
Moli 鹿降维提示：高压或失败时，搭档 Moli 鹿给出启发式线索（联想 / 词根 / 文化背景），绝不直接把翻译怼到脸上。
六维成长 + Moli 币：语萌小达人、人文小博士、环球游历家、智慧闯关王、暖心小使者、创美小艺术家六条成长轨；学习行为产出经验与 Moli 币，仅用于兑换装扮 / 道具 / 支线剧情，不可充值、不可交易。

🧠 系统架构
游戏内容由两个协作的 AI 智能体生成与把关：
智能体职责关键约束主笔智能体（Writer）生成场景叙事、三选项、视觉资产提示词输出纯净 JSON，含 narrative_text、options、visual_assets档案与规则智能体（E+F Agent）校验剧本、结算数值、存档仲裁检定阈值 ≤ 玩家词汇等级 +3；禁止凭空捏造道具；XP / 压力值平衡；防剧透
数据流：
玩家档案 (Player_Archive_State)  ┐
                                 ├──► 主笔 AI 生成剧本 ──► 仲裁 AI 校验 ──► PASS ──► 结算 & 存档 ──► 前端渲染
最新剧本 (Writer_Generated_JSON) ┘                                    └─ FAIL ──► 打回重写
仲裁 Agent 的「验尸报告」输出示例：
json{
  "validation_result": {
    "status": "FAIL",
    "error_codes": [
      "ERROR_01: 检定阈值[7]超过玩家当前能力上限",
      "ERROR_02: 捏造了不存在的物品[魔法法棍]"
    ]
  },
  "updated_archive": { }
}
🎨 视觉管线
剧本中的 visual_assets 携带英文绘图提示词，对接下游 AI 绘画节点（DALL·E 3 / Midjourney 等）：

场景背景 scene_background_prompt 与角色立绘 character_sprite_prompt
情绪光影联动：上升节点（Rise）用暖色明亮，下降节点（Fall）用高压阴影
角色立绘强制 white background，便于前端抠图叠加
提示词必须具象（1girl, holding a croissant, smiling），杜绝抽象文学描述

📚 教育与合规设计

寓教于乐：目标词汇自然融入对话场景并加粗，避免生硬说教
正向无惩罚：答错不扣数值，仅无额外奖励，保护学习积极性
零攀比：无排行榜、无战力对比，仅展示个人成长
家长可控：学习数据可查、兑换权限可设、每日目标可定、防沉迷强制休息
价值观中立：处理文化差异导向「和而不同」，内容贴合正版文化

🗂️ 仓库结构（建议）
moliverse/
├── src/
│   └── moli-french-game.jsx     # 前端游戏主程序（React）
├── agents/
│   ├── writer/                  # 主笔智能体 Prompt 与配置
│   └── arbiter/                 # 档案与规则智能体（E+F Agent）基准
├── content/
│   ├── scenes/                  # 剧情单元（澳门 / 巴黎 / 云南…）
│   └── characters/              # 人物与 NPC 设定
├── docs/
│   ├── growth-system.md         # 性格 + 六维成长 + Moli 币全案
│   └── qa-checklist.md          # 剧情与视觉质检审核手册
└── README.md
🚀 开发路线

阶段 1：性格选择 + 六维经验条 + Moli 币基础系统 + 装扮兑换
阶段 2：性格差异化剧情 / NPC 语气、分维度等级权益、主支线解锁
阶段 3：成就系统、综合等级全域解锁、家长管控、数值平衡
阶段 4：新城市场景持续迭代、节日限定、按反馈调优

📄 许可
待定。
