# 叶文哲 Wenzhe Ye

浙江工商大学软件工程专业，大二。做能跑起来、能验收的 AI 应用。

[![个人主页 wzye.top](https://img.shields.io/badge/%E4%B8%AA%E4%BA%BA%E4%B8%BB%E9%A1%B5-wzye.top-ff8a7a?style=for-the-badge)](https://wzye.top)

目前最主要的项目是知行有策，一个物业知识 AI Skill 生产平台。我是 13 人参赛团队的技术负责人，桌面端由我独立开发。

## 代表作：知行有策 · 物业知识 AI Skill 生产平台

[![知行有策宣传片封面，点击到个人主页观看宣传片](https://wzye.top/assets/zhixing/zhixing-promo-poster.jpg)](https://wzye.top)

把物业咨询的制度、方法、案例和专家经验拆成可溯源的知识原子，在 Skill 工厂里组装、评测、人工审核后上架，再由 Agent 按用户的问题编排多个 Skill，生成有依据的咨询报告，每条结论都能回到原文。

- **我的角色：** 技术负责人，桌面端独立开发；参加浙江省国际大学生创新大赛产业赛道
- **技术栈：** Electron · React · TypeScript · Vite · FastAPI · SQLite · DeepSeek · BGE
- **源码：** [brain898/zhixing-desktop](https://github.com/brain898/zhixing-desktop) ｜ **宣传片：** [在个人主页首屏观看](https://wzye.top)

**工程上解决的问题**

- **混合检索：** 关键词检索和 BGE 中文向量检索并行，用 RRF 融合排序。检索配置和索引都带版本号，同样的输入能复现同样的结果。
- **多 Skill 编排：** Agent 从已上架的 Skill 里按问题最多选 4 个顺序执行。缺必要信息时生成补问表单，计算类结论由程序复算，命中升级条件自动转人工。
- **失败可恢复：** 模型调用错误分类处理。网络、超时、限流自动重试；认证、权限、额度问题直接停止并给出原因。服务重启后恢复未完成的任务，从失败的步骤继续。
- **结论可追溯：** 报告的每条依据保存引用快照和原文摘录。Skill 版本更新或引用的知识失效时，自动暂停上架。
- **权限隔离：** 管理员与普通成员两级角色，咨询管理接口在服务端拒绝成员访问，不只是前端隐藏入口。
- **一键验收：** `python tests/acceptance.py full` 依次跑类型检查、生产构建、隔离业务测试和 Playwright 界面测试。测试库、上传目录和端口全部临时隔离，不碰业务数据；失败时保留日志、请求记录和截图。

## 其他作品

| 项目 | 做什么 | 技术 |
|---|---|---|
| [Forge 个人工作台](https://workbench.wzye.top/#daily-plan) | 每日计划、项目推进、学习记录、习惯与收入管理，用来安排我当天要做的事 | React, IndexedDB, PWA |
| [AI Daily](https://github.com/brain898/ai-daily) | 每天从 GitHub、HackerNews、Reddit、X 抓取 AI 资讯，大模型总结后生成结构化 Markdown 日报 | Python, 大模型 API, GitHub Actions |
| Gold Daily（源码未公开） | 每日抓取黄金市场数据，大模型生成分析并自动推送 | Python, 大模型 API, GitHub Actions |
| [问卷悬赏平台](https://survey.wzye.top/) | 发布问卷并设置悬赏金额的平台原型，尚未实际运营。[源码](https://github.com/brain898/survey-bounty) | Next.js, Supabase |

更早的小作品：[高等数学期末复习手册](https://gaoshu-notes.pages.dev)、[生日祝福互动页](https://challenge.wzye.top/)，合集见 [web-products](https://github.com/brain898/web-products)。

## Agent Skills

把反复用到的工作流封装成 Claude Code / Codex 可直接调用的 Skill。

- **[college-compass 大学罗盘](https://github.com/brain898/college-compass)：** 围绕求职、考研、专升本、保研、留学、考公六条路线的考察维度，判断一段经历对目标的价值，列出差距和下一步行动，每个判断写明依据。
- **[write-competition-research-reports](https://github.com/brain898/write-competition-research-reports)：** 把真实问卷、访谈和观察材料写成中文竞赛调研报告，支持起草、审稿、压缩和答辩风险检查，核心约束是结论强度不超过证据强度。
- **[super-forecaster](https://github.com/brain898/brain898/tree/master/skills/super-forecaster)：** 基于《超级预测》方法的决策辅助。拆解问题、找参考类数据、列反方理由，给出明确概率写进 Excel 决策账本，到期提醒回来结算。附 Python 脚本管理账本。

## 竞赛

- **2026 年温岭市「城市青年密码」大学生返乡实践项目大赛 一等奖**（油车配件企业新能源转型课题）。负责方向确定、访谈提纲设计、企业深访主访、调研报告撰写和最终答辩，并把报告写作流程整理成上面的开源 Skill。
- **浙江省国际大学生创新大赛产业赛道**：知行有策，见代表作。

## 技术栈

- **语言：** Python, TypeScript, JavaScript, C
- **前端与桌面：** React, Next.js, Electron, Vite, Tailwind CSS
- **后端与数据：** FastAPI, SQLite, Supabase, IndexedDB
- **AI：** DeepSeek API, BGE 向量检索, Agent Skills；用 Claude Code、Codex 辅助开发
- **测试与部署：** Playwright, GitHub Actions, Cloudflare Pages, Wrangler, PWA

---

更多作品和项目复盘在 [wzye.top](https://wzye.top)，欢迎交流。
