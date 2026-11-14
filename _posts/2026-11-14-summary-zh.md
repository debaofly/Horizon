---
layout: default
title: "Horizon Summary: 2026-11-14 (ZH)"
date: 2026-11-14
lang: zh
---

> 从 39 条内容中筛选出 10 条重要资讯。

---

**科技新闻**
1. [TorchTitan 在 384 块 GH200 上训练 1T 参数 MoE](#item-tech-news-1) ⭐️ 8.0/10
2. [上海通报交大医学院基因编辑事件调查结果](#item-tech-news-2) ⭐️ 8.0/10
3. [FAA 发布全国停飞令，故障原因仍未确认](#item-tech-news-3) ⭐️ 7.0/10
4. [ICML 2027 拟推两阶段审稿与投稿配额](#item-tech-news-4) ⭐️ 7.0/10
5. [微软 Outlook、Teams 与 Copilot 全球宕机逾 12 小时](#item-tech-news-5) ⭐️ 7.0/10
6. [DeepSeek 开放应用 API，整合搜索、文件与语音](#item-tech-news-6) ⭐️ 7.0/10
7. [OpenAI 推出 ChatGPT Wallet，支持美国 Pro 用户智能体支付](#item-tech-news-7) ⭐️ 7.0/10

**财经新闻**
1. [卢特尼克因英伟达芯片走私审查受质疑，其子领导公司申报持股近减半](#item-finance-news-1) ⭐️ 8.0/10
2. [芝加哥联储古尔斯比：美联储在通胀问题上“肯定还有工作要做”](#item-finance-news-2) ⭐️ 7.0/10
3. [黄仁勋辞职引发美中芯片管制收紧担忧](#item-finance-news-3) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [TorchTitan 在 384 块 GH200 上训练 1T 参数 MoE](https://www.reddit.com/r/MachineLearning/comments/1xvce5h/scaling_to_1t_moe_on_torchtitan_p/) ⭐️ 8.0/10

一位开发者在 Reddit 报告，其团队使用 TorchTitan 在 JUPITER 的 384 块 GH200 上训练约 1T 参数 MoE，达到约 1,300 tokens/s/GPU，相比最初起点提升 14 倍；这是团队自述结果，尚非独立复现。配置为 384 路 FSDP 加 4 路专家并行（EP），EP 严格限制在节点内，并刻意跳过流水并行（PP）以避免长流水气泡。报告还称，全量激活重计算带来 4 倍提升，GPU 端 Newton-Schulz 将优化器步从 42 秒降到约 2 秒，而按注意力成本分桶把最慢 rank 从平均的 7.9 倍降到 1.15 倍。作者称这些优化让共享 Hopper 集群上的前沿规模训练可行，但完整数据和外部细节在 Domyn/PyTorch 博客中。

reddit · r/MachineLearning · /u/f14-bertolotti · 11月13日 16:28

**「背景」** TorchTitan 是 PyTorch 面向大规模 LLM 训练的分布式训练框架；FSDP 把参数切片分散到各 rank 并在计算前聚合，EP 则让不同 GPU 持有不同专家、把 token 路由到对应专家。千亿至万亿参数 MoE 通常必须在多种并行方式间取舍，而 GH200 的跨节点 InfiniBand 带宽远低于节点内 NVLink，使通信成为主要约束。

**「影响」** 对在类似 InfiniBand 集群上复现的团队，最直接的限制是 EP 的 token all-to-all 必须留在节点内，否则约 25 GB/s 的跨节点带宽会压过计算；报告中的 bf16 专家梯度 all-to-all、FP8 all-gather 和节点内重分片都是围绕这一瓶颈设计的。另一个可操作检查是 FSDP 侧流上的分配器缓存：报告称把临时分配移到计算流并提前释放梯度后，384 个 rank 的分配重试全部消失、峰值保留内存减少 13.5 GiB。

**标签**: `#distributed training`, `#Mixture-of-Experts`, `#PyTorch`, `#GPU scaling`, `#large language models`

---

<a id="item-tech-news-2"></a>
### [上海通报交大医学院基因编辑事件调查结果](https://mp.weixin.qq.com/s/p0iC3tcI1yr10EBl2NjUvg) ⭐️ 8.0/10

上海公布对上海交通大学医学院一起定制基因编辑疗法致死事件的调查结果。涉事患儿确诊 Snijders Blok-Campeau 综合征，家属 2023 年联系仇某某团队定制疗法，2025 年 3 月注射后死于血栓性微血管病，相关论文于 2026 年 2 月发表在《自然》。调查认定临床前研究、伦理审查和知情同意存在缺陷，部分人员收受家属财物约 106 万元；仇某某、杨某被开除并取消资格 5 年，相关机构被约谈整改并受行政处罚。

telegram · zaihuapd · 11月13日 09:24

**「背景」** 基因编辑疗法在用于患者前，通常须完成临床前研究、通过伦理审查并取得知情同意，以评估安全性并保障受试者权益。此次事件涉及的是一种针对个别患者的定制基因编辑治疗，这类治疗不按标准化临床试验的常规入组路径推进，因此上述前置环节是否充分成为调查重点。

**「影响」** 对开展个体化基因编辑疗法的研究机构和临床团队而言，这一调查将临床前研究、伦理审查和知情同意列为被追责的缺陷环节；涉事人员被开除并取消资格 5 年，机构被约谈整改和行政处罚。

**标签**: `#gene editing`, `#research ethics`, `#clinical trials`, `#biotech regulation`, `#scientific misconduct`

---

<a id="item-tech-news-3"></a>
### [FAA 发布全国停飞令，故障原因仍未确认](https://www.nbcnews.com/news/us-news/faa-orders-nationwide-ground-stop-departing-flights-reasons-safety-rcna609247) ⭐️ 7.0/10

美国联邦航空管理局（FAA）于 2026 年 11 月 13 日发布全国范围的停飞令，暂停出发航班。官方尚未完整说明原因；有评论引用《华尔街日报》的报道称，故障似乎影响由 L3Harris Technologies 负责的通信网络，该网络承载空管员与飞行员通话所需的关键无线电频率，但是否波及雷达数据仍不清楚。评论中的后续信息并不一致：有人引用《纽约时报》称停飞令已解除，也有人引用国土安全部官员的话称故障可能持续较长时间。

hackernews · zulln · 11月13日 21:05 · [社区讨论](https://news.ycombinator.com/item?id=50489641)

**「背景」** 此次停飞由通信故障触发：据 Al Jazeera 报道，故障影响全部 22 个区域空管中心；《卫报》援引知情人士称，受影响的是由 L3Harris Technologies 负责、用于空管员与飞行员通话的关键无线电网络。FAA 此前已宣布将 AI 航线管理工具 SMART 扩展至全国空域，但明确表示该工具只提供建议，不能取代空管员或接管飞机；社区中把两者联系起来的说法目前没有证据支持。

**「实际影响」** 全国停飞直接打乱了计划从美国机场起飞的旅客行程：CNN 报道称，停飞期间航班取消数量持续上升，官方起初没有给出恢复时间；CNBC 随后报道，停飞约四小时后解除，但已影响数千架次离港航班。停飞令解除后，旅客仍需向航空公司确认航班状态，因为积压和取消不会立即消失。

**「社区讨论」** 评论区对原因存在明显分歧：一种说法指向 L3Harris 负责的空管通信网络故障，另一种则猜测这与 FAA 近期宣布在全国 22 个中心推广的 AI 空管系统“SMART”有关，但后者只是未经证实的推测。也有评论抱怨官方信息稀少、机场出发信息显示不一致，并同时出现“停飞令已解除”和“可能延长”两种后续说法。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.aljazeera.com/news/liveblog/2026/11/13/groundling-live">LIVE: FAA issues US ground stop , some international... | Al Jazeera</a></li>
<li><a href="https://www.theguardian.com/us-news/live/2026/nov/13/us-politics-latest-news-updates-democrats-republicans-donald-trump-van-hollen-chuck-schumer">US flight outage live updates: FAA grounds thousands... | The Guardian</a></li>
<li><a href="https://arstechnica.com/ai/2026/11/faa-expands-ai-advice-to-manage-air-traffic-congestion-across-entire-us-airspace/">FAA expands AI advice to manage air traffic ... - Ars Technica</a></li>
<li><a href="https://gizmodo.com/the-faa-is-rolling-out-its-ai-air-traffic-tool-nationwide-2000839347">The FAA Is Rolling Out Its AI Air Traffic Tool Nationwide</a></li>
<li><a href="https://www.cnn.com/2026/11/13/us/live-news/flights-ground-stop-faa">Live updates on FAA ground stop : No timeline for resolution as flight ...</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/faa-ground-stop.html">FAA lifts ground stop after four hours, but flight cancellations will...</a></li>

</ul>
</details>

**标签**: `#FAA ground stop`, `#critical infrastructure`, `#air traffic control`, `#telecommunications outage`, `#AI-ATC speculation`

---

<a id="item-tech-news-4"></a>
### [ICML 2027 拟推两阶段审稿与投稿配额](https://www.reddit.com/r/MachineLearning/comments/1xvkxbj/icml_2027_changes_d/) ⭐️ 7.0/10

一篇 Reddit 帖子根据 ICML 2027 征稿通知总结称，会议将采用两阶段审稿：由领域主席决定论文是否进入完整评审，任何第一阶段拒稿须经高级领域主席确认，作者可在 2 月 23 日前收到简短理由。投稿限制包括每人最多出现在 20 份投稿中、每篇论文须从作者名单中指定一名互惠审稿人且每位审稿人最多承担 6 篇、投稿达到 3 篇及以上者须加入程序委员会；不合规论文可能被直接拒稿。帖子特别提到，每位作者最多只能有一篇论文在作者中没有合格互惠审稿人，这被视为限制“挂名”投稿的关键变化；上述内容来自 Reddit 对 CFP 的转述，而非官方公告原文。

reddit · r/MachineLearning · /u/Gravitist · 11月13日 21:53

**「背景」** ICML 是机器学习领域的主要学术会议，录用决定依赖程序委员会（PC）以及领域主席和高级领域主席的同行评审。随着投稿量持续膨胀，会议长期面临审稿人负担过重的问题；此次 2027 年征稿政策正是试图通过限制作者投稿数量和强制互惠审稿来缓解这一矛盾。

**「影响」** 对作者而言，最直接的影响是提交前必须把“可审稿的合著者”当作配额来规划：每篇论文都要从作者名单中指定一名互惠审稿人，单名审稿人最多覆盖 6 篇；每位作者最多只能有一篇论文没有任何合格互惠审稿人，不合规论文可能被 desk reject。拥有 3 篇及以上投稿的作者还必须加入程序委员会，因此多投团队需要提前分配审稿人力，而不能只在截止日前临时加名。

**标签**: `#ICML`, `#peer review`, `#ML research`, `#conference policy`, `#submission limits`

---

<a id="item-tech-news-5"></a>
### [微软 Outlook、Teams 与 Copilot 全球宕机逾 12 小时](https://www.reuters.com/technology/microsoft-365-outlook-down-thousands-us-users-downdetector-shows-2026-11-12/) ⭐️ 7.0/10

微软 Outlook、Teams 和 Copilot 在 11 月 13 日仍处于宕机状态，故障已持续超过 12 小时，打乱全球企业与政府的通信。微软称原因是服务器问题，未发现恶意活动，并表示已扩大修复范围、看到回稳迹象。澳大利亚、日本和美国部分政府机构受到影响，Euronext 的邮件受阻，台湾有金融机构改用传真确认交易；这是 Microsoft 365 服务今年第二次中断。

telegram · zaihuapd · 11月13日 12:21

**「背景」** Outlook、Teams 和 Copilot 都属于 Microsoft 365 云端服务，服务端故障会同时影响邮件、协作和 AI 功能，而不只是单一客户端的问题。此次中断还波及 OpenAI 和 Anthropic 使用的微软连接器，OpenAI 表示正在排查新建连接失败和工具调用异常，显示依赖 Microsoft 365 的第三方 AI 服务也会被连带影响。

**「影响」** 故障期间，部分机构启动了备用流程：台湾金融机构改用传真确认交易，Euronext 的邮件通信受阻。对依赖 Outlook、Teams 和 Copilot 的企业与政府用户而言，关键通信和协作需要准备降级方案，而不能只依赖 Microsoft 365。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.aljazeera.com/news/liveblog/2026/11/13/live-microsoft-struggles-to-restore-services-as-outage-hits-global-users">Microsoft outage live: Global users affected as services... | Al Jazeera</a></li>
<li><a href="https://www.theguardian.com/technology/2026/nov/13/microsoft-outage-outlook-teams-word-excel-reports">Microsoft scrambles to fix global outage affecting Teams and Outlook</a></li>

</ul>
</details>

**标签**: `#Microsoft 365`, `#outage`, `#cloud reliability`, `#enterprise software`, `#incident response`

---

<a id="item-tech-news-6"></a>
### [DeepSeek 开放应用 API，整合搜索、文件与语音](https://mp.weixin.qq.com/s/78KBHc4-4N5b2vfL9SkutQ) ⭐️ 7.0/10

DeepSeek 面向开发者开放应用型 API：在原有 API 中开启对应参数，即可获得深度思考搜索、文件输入、阅读链接和语音等对话能力，工具调用与上下文拼接由服务端自动完成。V4.1-Flash 模型已在三个接口中支持这些能力；Search、Fetch、OCR、ASR、TTS 也可单独调用，官方同时开源了可导入历史对话的前端 Demo（deepseek-ai/chat-demo）。上述内容来自 Telegram 转发，尚缺独立验证和更完整的技术细节。

telegram · zaihuapd · 11月13日 14:27

**「背景」** 所谓应用型 API，是把搜索、网页抓取、OCR、语音识别与合成等工具放到服务端编排；开发者只需在原有对话接口中开启参数，不必自行串接各项服务。DeepSeek 官方文档称，App 背后的这些能力现已通过 API 提供，OCR、ASR、TTS 也可单独调用。

**「影响」** 开发者可以直接调用组合 API 获得搜索、文件读取和语音能力，也可按需单独调用 Search、Fetch、OCR、ASR、TTS，减少自行拼接多条能力链路的工程量。接入时需按不同接口和参数启用相应能力，现有 API 集成应检查与 V4.1-Flash 三个接口的兼容性；开源的 chat-demo 还提供了导入历史对话并将其用于本地部署网页端的路径。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://api-docs.deepseek.com/news/news261113/">The full DeepSeek App experience, now via API | DeepSeek API Docs</a></li>

</ul>
</details>

**标签**: `#DeepSeek`, `#AI APIs`, `#multimodal AI`, `#tool calling`, `#open-source demo`

---

<a id="item-tech-news-7"></a>
### [OpenAI 推出 ChatGPT Wallet，支持美国 Pro 用户智能体支付](https://openai.com/index/introducing-chatgpt-wallet/) ⭐️ 7.0/10

OpenAI 宣布推出 ChatGPT Wallet，并表示即日起在美国向 18 岁以上的 ChatGPT Pro 订阅用户开放，且用户需使用美国发行的银行卡。该钱包与美国运通、万事达和 Visa 合作，支付网络向智能体下发替代真实卡号的支付令牌，使智能体付款时无需接触用户的真实卡号。每笔购买前，用户要在 ChatGPT 内核对商品和金额，并通过 Face ID 或指纹完成验证。

telegram · zaihuapd · 11月13日 15:43

**「背景」** ChatGPT Wallet 面向的是智能体代为结账的场景：由代理发起购买，用户再逐笔授权，因此支付凭证不能直接暴露真实卡号。卡组织的网络令牌化会用替代值取代卡号，降低代理链路泄露卡信息的风险。OpenAI 表示该钱包与运通、万事达和 Visa 合作，初期通过 dots 面向美国 ChatGPT Pro 订阅者开放。

**「影响」** 按当前流程，逐笔生物识别确认意味着智能体无法在用户不参与的情况下完成购买；用户每次支付都必须到场核对商品和金额，安全性与自动化便利性因此需要权衡。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://openai.com/index/introducing-chatgpt-wallet/">Introducing ChatGPT Wallet | OpenAI</a></li>

</ul>
</details>

**标签**: `#OpenAI`, `#AI agents`, `#payments`, `#fintech`, `#security`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [卢特尼克因英伟达芯片走私审查受质疑，其子领导公司申报持股近减半](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 8.0/10

美国商务部长霍华德·卢特尼克因据 Axios 报道曾多次抵制对疑似英伟达芯片走私中国的打击而面临审视；CNBC 分析证券申报文件发现，他此前经营、现由其子布兰登和凯尔领导的 Cantor Fitzgerald 在 2025 年 9 月至 2026 年 3 月间申报的英伟达持股数量下降 49%，从逾 350 万股降至 178 万股（不含期权），但 Cantor 称其在英伟达的自营头寸规模不大，而申报中的头寸与客户互换交易有关。英伟达 CEO 黄仁勋于周四辞职。

rss · CNBC Finance · 11月13日 23:42

**「背景」** 美国自 2022 年起以国家安全为由限制对华出口最先进人工智能芯片，但这类出口管制一直难以执行。据 NBC News 报道，英伟达 CEO 黄仁勋在出现涉及与中国疑似间谍的婚外情报道后辞职，令商务部长鲁特尼克及其子所领导的 Cantor Fitzgerald 与英伟达的关系再受审视。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.bbc.com/news/articles/c67429m3vem3o">How a sex scandal at Nvidia is putting pressure on the White House</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html">Howard Lutnick’s sons’ Nvidia ties amid Jensen Huang China spy ...</a></li>
<li><a href="https://www.nbcnews.com/tech/tech-news/nvidia-ceo-jensen-huang-resigns-reports-extramarital-relationships-rcna608402">Nvidia CEO Jensen Huang resigns after reports of affair and...</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#Howard Lutnick`, `#Cantor Fitzgerald`, `#US-China export controls`, `#conflict of interest`

---

<a id="item-finance-news-2"></a>
### [芝加哥联储古尔斯比：美联储在通胀问题上“肯定还有工作要做”](https://www.cnbc.com/2026/11/13/chicago-feds-goolsbee-says-central-bank-has-definitely-got-work-to-do-on-inflation.html) ⭐️ 7.0/10

芝加哥联储主席古尔斯比 11 月 13 日表示，美联储在通胀问题上“肯定还有工作要做”，需要继续重建公信力；此前公布的 10 月生产者价格指数（PPI，批发价格指标）同比上涨 6.5%，为 2022 年 11 月以来最高。市场已完全计入美联储在 12 月 8 日至 9 日会议上加息 25 个基点的预期。

rss · CNBC Finance · 11月13日 14:22

**「背景」** 美联储的通胀目标是 2%，古尔斯比称通胀已近六年高于该目标、近期没有进展；他目前不是联邦公开市场委员会（FOMC）投票委员，2027 年才拥有投票权。

**标签**: `#Federal Reserve`, `#inflation`, `#PPI`, `#interest rates`, `#monetary policy`

---

<a id="item-finance-news-3"></a>
### [黄仁勋辞职引发美中芯片管制收紧担忧](https://www.cnbc.com/2026/11/13/jensen-huang-nvidia-us-china-relations.html) ⭐️ 7.0/10

英伟达 CEO 黄仁勋在国会审查其与一名被指为中国间谍的女性的婚外情期间辞职，并同意在 11 月 26 日前作证；分析人士预计，这可能促使美国在 2026 年底前进一步收紧对华芯片出口管制。

rss · CNBC Finance · 11月13日 02:56

**「背景」** 美国自 2022 年起限制英伟达向中国出售先进芯片，特朗普政府 2025 年放宽了部分拜登时期限制，两国目前维持脆弱的贸易休战。

**「影响」** 分析人士警告，若国会收紧管制，中国科技企业获取美国先进芯片将更困难，北京也可能以限制稀土或芯片制造材料供应作为反制。

**标签**: `#US-China relations`, `#Nvidia`, `#semiconductor export controls`, `#Congressional scrutiny`, `#AI competition`

---