# Super Forecaster · 决策概率账本

> 把你脑子里"我应该……"的纠结，逼成一道**写进账本、到期结算**的概率题。

![type](https://img.shields.io/badge/type-decision%20forecasting-blue)
![runtime](https://img.shields.io/badge/runtime-Claude%20Code%20%7C%20Codex%20%7C%20OpenClaw-green)
![method](https://img.shields.io/badge/method-Fermi%20%2B%20Reference%20Class%20%2B%20Bayes-orange)

![一次完整对话演示](assets/super-forecaster-demo.gif)

> 一次完整对话：从"要不要去这份实习"到写进账本、建好到期提醒，20 秒走完 8 步。

市面上叫 "forecasting" 的工具几乎都在预测**销量、股价、时间序列**。
这个 skill 预测的是**你自己**：要不要去这家实习、值不值得买这门课、这个方向该不该转——
然后把预测记进账本，到期回来看自己当初算得准不准。

---

## 你什么时候需要它？

- **实习/offer 二选一**："A 和 B 我该去哪个？" → 拆成"哪个 3 个月内更可能给我可写简历的 case"
- **付费决策**："这门 499 的课值不值？" → 拆成可结算的子问题 + 找参考类数据，不靠讲师话术
- **方向纠结**："要不要转/要不要 all in X？" → 拦住"我应该"的情绪话术，给一个能被打脸的概率

一句话：**当你说"我应该 / 一定要 / 肯定" 的时候，它会拦你一下，然后逼你算账。**

## 它会交付什么？

1. **一道结算化的概率题**：把云状纠结拆成 2–4 个有截止日、可 yes/no 判定的子问题，每个给单值概率（`P = 42%`，不是"大概率"）。
2. **一行决策账本**：自动追加进 `decisions.xlsx`（日期/题目/费米化子问题/概率/截止日/参考类来源/反方理由/实际结果/反思）。
3. **到期复盘提醒**：到截止日前一天提醒你回来结算——这是"超级预测"的灵魂，**敢被打脸才能校准**。

## 快速开始

```bash
# 1. 放进任意 skill 目录（按你的 runtime 选其一）
#    Claude Code:  ~/.claude/skills/super-forecaster/
#    牛马AI:        ~/.newmax/skills/super-forecaster/
#    Codex:        ~/.codex/skills/super-forecaster/

# 2. 脚本依赖（写账本用）
pip install openpyxl

# 3. 直接对 Agent 说话即可触发（见下）
```

账本路径可配置，**不写死任何绝对路径**：环境变量 `DECISIONS_XLSX` > 首次使用时你指定的位置 > 默认 `./decisions.xlsx`。

## 触发方式

直接说人话就行：

- "我在纠结要不要接这份实习"
- "这门课值不值得买"
- "3 个月内我能不能做出 X，概率多大"
- "帮我判断一下该选 A 还是 B"
- "上次那条预测到期了，结算一下"
- "过去 30 天我哪些预测被打脸了"

## 示例

**输入**："我手上有第二份实习邀约，AI 应用方向，远程，但日薪没说。要不要去？"

**过程**（8 步，不跳步）：判断走不走 → 反问拆出底层真问题 → 费米化成 3 个带截止日的子问题 → web_search 找参考类（搜不全则给 BROK 提示词丢豆包）→ 问你的特殊性微调 → 给 2–3 条具体到机制的反方 → 出单值概率 → 写账本 → 建到期提醒。

**输出片段**：
```
Q1（接触 LLM API 业务）：P = 62%
Q2（拿到可写简历的 case）：P = 38%
Q3（公开可展示链接）：P = 25%
你的最终概率（你来填）：__
[账本] 已追加到 decisions.xlsx 第 N 行
[提醒] 已建定时任务 3 个
```

完整逐步演示见 [`references/example_session.md`](references/example_session.md)。

## 它和同类有什么不同？

| | 时间序列/财务 forecasting skill | **Super Forecaster** |
|---|---|---|
| 预测对象 | 销量、股价、外部数据 | **你自己的个人决策** |
| 方法 | ARIMA / Prophet / 回归 | 费米化 + 参考类 + 贝叶斯（Tetlock 路线）|
| 产物 | 预测曲线、置信区间 | **可结算的决策账本 + 到期复盘** |
| 谁判定对错 | 等下一批数据 | **到期你自己打脸自己，可校准** |

## 安全边界

- **不替你决策**：它给预测（概率），不替你下"做/不做"，也不替你填最终概率。
- **不许编**：没有参考类宁可说"算不出"，不编一个看起来合理的数字；引用豆包结果会标注"未独立验证"。
- **不主动读你的隐私**：不主动读你的个人价值观/目标档案，避免锚定基础概率。
- **不骚扰**：措辞拦截每轮 ≤ 2–3 次，魔鬼代言人只触发一次。
- 用户中途说"不算了"立刻停。

## 文件结构

```
super-forecaster/
├── SKILL.md                      # 角色/输入/8步流程/输出格式/护栏/例子
├── README.md                     # 本文件
├── references/
│   ├── methodology.md            # 费米化/参考类/贝叶斯速记（用户问"为什么"时引用）
│   ├── brok_template.md          # BROK 豆包提示词模板（参考类第二段）
│   └── example_session.md        # 完整 8 步流程演示
├── scripts/
│   ├── init_ledger.py            # 初始化空账本（自动建表头）
│   ├── append_decision.py        # 追加一条预测到 decisions.xlsx
│   └── settle_decision.py        # 到期结算 + 算 Brier 分数和校准曲线
├── assets/
│   └── super-forecaster-demo.gif # 一次完整对话的 20s 演示
└── test-prompts.json             # 验证用例
```

## 工具依赖与降级

| 能力 | 首选 | 不可用时降级 |
|---|---|---|
| 参考类联网搜索 | `mcp__web-search__web_search` | 生成 BROK 提示词，让用户拿去豆包/Kimi 等任意联网助手手动搜，粘回结果 |
| 到期复盘提醒 | `mcp__scheduled-tasks__create_scheduled_task` | 把截止日清单输出给用户，让其手动设日历提醒 |
| 写账本 | `openpyxl`（Python） | 缺库时提示 `pip install openpyxl`；仍不可用则以 markdown 表格输出账本行 |

## 复盘与校准（灵魂功能）

预测不结算 = 算命。到期回来看自己准不准，才是"超级预测"：

```bash
python scripts/settle_decision.py --xlsx ./decisions.xlsx --list-due      # 列出到期未结算
python scripts/settle_decision.py --xlsx ./decisions.xlsx --settle --row 7 --result no --reflection "高估了任务密度"
python scripts/settle_decision.py --xlsx ./decisions.xlsx --calibrate     # 算 Brier 分数 + 分桶命中率
```

`--calibrate` 输出示例：
```
校准报告（样本 n=6）
  Brier 分数：0.265  （越低越好，0=完美，0.25=瞎猜）
  概率分桶 vs 实际命中率：
    [60%-80%) n= 2 实际命中=50% （过度自信）
    [80%-100%) n=2 实际命中=50% （过度自信）
```
当你看到"我标 80% 的事其实只发生 50%"，你就知道自己系统性过度自信了——这正是 skill 的价值。

## 验证与测试

测试用例见 [`test-prompts.json`](test-prompts.json)，覆盖：简单决策应被步骤0挡掉、模糊纠结应跑完整流程、措辞陷阱应被拦截。
