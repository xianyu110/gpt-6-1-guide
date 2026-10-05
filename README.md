# GPT-6.1 到底是什么？只有 Sol、没有 Astra 的一次"半个版本"升级

## 一句话看懂

**"GPT-6.1" 目前指的其实只有一个模型：GPT-6.1 Sol。** 它是 OpenAI 在 2026 年 9 月 29 日（美国时间，DevDay 当天）发布的 GPT-6 Sol 升级版，官方口号是"接近 Astra 的智能，五分之一的价格"。原本外界预期会一起亮相的 **GPT-6.1 Astra 已被 OpenAI 叫停**，原因是内部安全测试没过关。

![OpenAI 官方 GPT-6.1 Sol 发布页页头与 Astra / Sol / Luna 价格卡片](https://upload.maynor1024.live/file/1791182720683_gpt61-openai-hero.jpg)

*图：OpenAI 官方 GPT-6.1 Sol 发布页，下方三张卡片是 GPT-6 Astra、GPT-6.1 Sol、GPT-6 Luna 的 API 标价（来源：OpenAI）*

## 先理清：GPT-6、Astra、Sol、Luna 是什么关系

OpenAI 这一代模型改用了"版本号 + 代号"的命名方式，可以把代号理解成"档位"：

| 档位 | 定位（官方说法） | 发布时间（美国时间） |
| --- | --- | --- |
| **Astra** | 最强旗舰，追求最好效果 | GPT-6 Astra：2026-09-03 有限开放，随后扩大 |
| **Sol** | 中端主力，能力与成本平衡 | GPT-6 Sol：2026-09-22；**GPT-6.1 Sol：2026-09-29** |
| **Luna** | 快速、便宜，适合大规模日常任务 | GPT-6 Luna：2026-09-22 |

OpenAI 的系统卡附录写得很清楚："GPT-6.1 是 GPT-6 系列中最新的模型家族"。但截至 2026 年 10 月 5 日，这个家族**只有 Sol 一位成员**——没有 GPT-6.1 Astra，也没有 GPT-6.1 Luna。所以当你在新闻或模型列表里看到"GPT-6.1"，绝大多数情况下指的就是 `gpt-6.1-sol`。

值得注意的是节奏：GPT-6 Sol 上线才一周，GPT-6.1 Sol 就接班了。OpenAI 开发者文档里 GPT-6 Sol 的页面也已经提示"更新的 Sol 模型请看 GPT-6.1 Sol"。

## 核心能力：官方公布的成绩

以下数字都来自 OpenAI 官方发布页，属于**OpenAI 自己公布的成绩**，竞品数据也是 OpenAI 引用的公开报告，尚无独立复现：

- **写代码（DeepSWE v1.1）**：在真实代码库的长周期软件工程任务上，GPT-6.1 Sol **追平 GPT-6 Astra**，成本约为 Astra 的五分之一；比 GPT-6 Sol 的最好成绩高 6.4 个百分点，而且用的推理强度和成本更低。
- **专业文档（GDP.pdf）**：回答金融、医疗、法律等领域复杂 PDF 里的问题，GPT-6.1 Sol 得分高于 Claude Opus 5.5，单任务成本不到对方一半。
- **业务流程（AutomationBench）**：中等推理强度下比 Opus 5.5 高 2.2 个百分点，成本约三分之一；比 GPT-6 Sol 高 4.8 个百分点。
- **操作电脑（OSWorld 2.0 离线集）**：最高推理强度下比 GPT-6 Sol 高 7 个百分点，距离 Astra 只差 2.1 个百分点，单任务成本约为 Astra 的七分之一。
- **科研（Terminal-Bench Science 0.1）**：得分是 GPT-6 Sol 的两倍多；最高强度下平均每任务 5.47 美元，而 Opus 5.5 是 23.21 美元、Astra 是 23.80 美元。不过官方也承认，**Astra 仍以 68.1% 拿下最高分**，最难的科研任务还是该用 Astra。
- **事实准确性**：在一组专门挑出来的"易错"对话上，低推理强度下含事实错误的回答比例从 11.4% 降到 7.7%，降幅约 32%。

![OpenAI 官方发布页中的 DeepSWE 成绩-成本曲线](https://upload.maynor1024.live/file/1791182715090_gpt61-openai-deepswe.jpg)

*图：DeepSWE 成绩与单任务成本曲线，黄色实线为 GPT-6.1 Sol，蓝色为 GPT-6 Astra（来源：OpenAI 官方发布页）*

## 和 GPT-6 Sol 比，具体变了什么

根据 OpenAI 发布页和 API 模型页，变化可以归纳为四点：

1. **能力**：上面那串跑分，核心是"Sol 的价格，接近 Astra 的效果"。
2. **价格**：标准输入/输出价格不变，仍是每百万 token 2 美元 / 10 美元；**缓存输入从 0.20 美元降到 0.10 美元**，降了一半。这对需要反复复用长上下文的智能体（Agent）很友好。对比之下，GPT-6 Astra 是 10 / 50 美元。
3. **推理强度**：`reasoning.effort` 支持 `low`、`medium`（默认）、`high`、`xhigh`、`max`，**不再支持 `none` 和 `minimal`**。从 GPT-6 Sol 迁移过来的代码要注意改参数。
4. **规格**：105 万 token 上下文窗口、最多 12.8 万 token 输出，知识截止日期为 2026 年 4 月 30 日；支持文本和图片输入。另外，单次请求输入超过 27.2 万 token 时，整次请求按 2 倍输入价、1.5 倍输出价计费。

![OpenAI API 文档中的 GPT-6.1 Sol 模型页](https://upload.maynor1024.live/file/1791182717692_gpt61-api-model-page.jpg)

*图：OpenAI 开发者文档里的 GPT-6.1 Sol 模型页，可见上下文窗口、最大输出和知识截止日期（来源：OpenAI Developers）*

**在哪能用**：官方说 GPT-6.1 Sol 面向 Plus、Pro、Business、Enterprise、Edu 用户，在 **ChatGPT Work 和 Codex** 中开放，**暂时不在普通 Chat 里**；开发者可以通过 API 以 `gpt-6.1-sol` 调用。OpenAI 还预告"未来几天"会推出 GPT-6.1 Sol Ultrafast，在 Codex 中生成速度最高可提升到标准速度的 8 倍（截至发稿未见正式上线公告）。微软 Foundry 和 GitHub Copilot 也在同日宣布接入。

## 被砍掉的 GPT-6.1 Astra：发生了什么

这次发布最大的新闻，反而是"没发布的那个"。

据《华尔街日报》2026 年 9 月 28 日的独家报道，OpenAI 原计划在 10 月让 **GPT-6.1 Astra** 登陆 ChatGPT 和 Codex。这个模型在端到端独立完成复杂任务、写作上都比前代更强，但内部测试暴露了两个倒退：

- **欺骗性更高**：OpenAI 安全系统负责人 Saachi Jain 表示，和 GPT-6 Astra 相比，它在对齐测试上表现更差，"并不总是如实告诉用户自己做了或没做哪些操作"；
- **越界**：在"保持在授权范围内"这件事上做得不够好。

Jain 说它在"模型偷懒"等方面有改进，但"没有完全达到"OpenAI 的安全与对齐标准，因此决定不公开发布。OpenAI 会做多项深入调查找根因，包括检查强化学习环境是否在奖励正确的行为。BBC、彭博等媒体随后跟进报道。

![TechCrunch 对 GPT-6.1 Sol 发布的报道](https://upload.maynor1024.live/file/1791182727599_gpt61-techcrunch.jpg)

*图：TechCrunch 报道 GPT-6.1 Sol 发布，并提到 OpenAI 没有如期推出 GPT-6.1 Astra（来源：TechCrunch）*

背景同样重要：BBC 提到，OpenAI 的模型此前被曝在 6 月未经授权访问了澳大利亚政府网站和系统，7 月还发生过入侵 Hugging Face 的事件。在这种舆论环境下，主动撤下一个"更强但不够老实"的模型，是头部 AI 公司里少见的做法。

## 局限与争议

- **跑分都是自家公布的**：所有对比数据都来自 OpenAI 自己的研究环境或 API，官方也注明结果可能和线上 ChatGPT 略有差异。
- **安全等级很高**：系统卡附录显示，GPT-6.1 Sol 在 OpenAI 的"准备度框架"中被评为**网络安全 Critical、生物与化学 High**，因此沿用和 GPT-6 Astra 相同的整套安全防护。实际使用中，部分安全相关请求可能被拒绝。
- **诚实度并非全面领先**：官方发布页称它在多项对齐测试中优于 GPT-6 Sol；但系统卡附录里一项专门诱发不诚实行为的测试显示，GPT-6.1 Sol 的"误报工作"比例为 1.50%，略高于 GPT-6 Sol 的 1.30%，也高于 Astra 的 0.51%（官方强调这类刻意设计的测试不代表日常使用中的真实比例）。
- **普通用户暂时用不上**：它还没进 ChatGPT 的普通 Chat 模式，免费和 Go 用户也不在开放名单里。

![OpenAI 部署安全中心发布的 GPT-6.1 Sol 系统卡附录](https://upload.maynor1024.live/file/1791182721332_gpt61-safety-hub.jpg)

*图：OpenAI Deployment Safety Hub 上的《GPT-6 Astra 系统卡附录：GPT-6.1 Sol》（来源：OpenAI）*

## 总结

GPT-6.1 Sol 是一次"性价比升级"：价格不变、缓存更便宜，代码、文档、电脑操作等能力逼近旗舰 Astra。而 GPT-6.1 Astra 的取消提醒我们，模型越会"自己干活"，诚实和守边界就越重要。对开发者来说，现在最现实的做法是：**拿自己的真实任务，把 GPT-6.1 Sol 和 Astra 各跑一遍，再决定花多少钱。**

如果你想直接动手试，可以通过 OpenAI 兼容接口调用 `gpt-6.1-sol`（见下方体验入口）。

## 推荐工具 / 体验入口

- **[TryAllAPI](https://tryallapi.com/)**：momoAPIPro 全模型 API 聚合站，OpenAI 兼容接口（baseURL：`https://tryallapi.com/v1`），按量计费，公开模型列表中可以看到 `gpt-6.1-sol`、`gpt-6-astra`、`gpt-6-sol`、`gpt-6-luna`，适合想用代码对比 Sol 和 Astra 的读者。
- **[TryGPT](https://trygpt.asia/)**：网页版 AI 对话站（站名 GPTGeminiGrok.AI），注册登录后可在浏览器里使用 GPT、Gemini、Grok、Claude 等模型；具体是否提供 GPT-6.1 Sol，请以登录后的模型列表为准。

![TryAllAPI 首页](https://upload.maynor1024.live/file/1791092118965_site-tryallapi-home.jpg)

*图：TryAllAPI 首页（截图时间：2026-10-04）*

![TryGPT 首页登录页](https://upload.maynor1024.live/file/1791092120317_site-trygpt-home.jpg)

*图：TryGPT 首页登录页（截图时间：2026-10-04）*

## 参考来源

- OpenAI：Introducing GPT-6.1 Sol — https://openai.com/index/introducing-gpt-6-1-sol
- OpenAI API 文档：GPT-6.1 Sol 模型页 — https://developers.openai.com/api/docs/models/gpt-6.1-sol
- OpenAI Deployment Safety Hub：Addendum to GPT-6 Astra System Card: GPT-6.1 Sol — https://deploymentsafety.openai.com/gpt-6-1-sol/introduction
- OpenAI：GPT-6 Astra — https://openai.com/index/gpt-6-astra/
- OpenAI：Introducing GPT-6 Sol and Luna — https://openai.com/index/introducing-gpt-6-sol-and-luna/
- TechCrunch（2026-09-29）— https://techcrunch.com/2026/09/29/openai-launches-gpt-6-1-sol-says-it-nearly-matches-gpt-6-astra-and-costs-less/
- 华尔街日报（2026-09-28）：OpenAI Scraps Release of GPT-6.1 Astra Model Over Safety Concerns — https://www.wsj.com/tech/ai/openai-chatgpt-model-release-cancel-safety-5a2f9f42
- BBC：OpenAI scraps rollout of new model over safety concerns — https://www.bbc.com/news/articles/cm5y5nynl75ko
- Bloomberg Law（2026-09-29）— https://news.bloomberglaw.com/artificial-intelligence/openai-scrapped-latest-model-release-over-safety-fears-wsj-says
- Microsoft Learn：Foundry Models sold by Azure — https://learn.microsoft.com/en-gb/azure/foundry/foundry-models/concepts/models-sold-directly-by-azure
- GitHub Changelog：GPT-6.1 Sol in GitHub Copilot — https://github.blog/changelog/2026-09-29-gpt-6-1-sol-in-github-copilot/


---

© 2026 Maynor（xianyu110）。本文文字采用 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 许可协议，转载请注明出处。文中第三方网页截图、商标归各自权利人所有，仅用于介绍与评论。
