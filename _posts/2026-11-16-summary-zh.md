---
layout: default
title: "Horizon Summary: 2026-11-16 (ZH)"
date: 2026-11-16
lang: zh
---

> 从 36 条内容中筛选出 8 条重要资讯。

---

**科技新闻**
1. [Meta FAIR 与 NYU 用 200+ 模型拆解多模态视觉编码器](#item-tech-news-1) ⭐️ 8.0/10
2. [美团开放 LongCat-2.5 权重，称训练未用英伟达 GPU](#item-tech-news-2) ⭐️ 8.0/10
3. [MacBook Pro OLED 屏幕的 PWM 频闪问题](#item-tech-news-3) ⭐️ 7.0/10
4. [Protomaps 自托管地图瓦片的成本与限制](#item-tech-news-4) ⭐️ 7.0/10
5. [Raschka 解析现代大语言模型的位置嵌入](#item-tech-news-5) ⭐️ 7.0/10

**财经新闻**
1. [CNBC：卢特尼克因英伟达持股与融资关系面临伦理质疑](#item-finance-news-1) ⭐️ 8.0/10
2. [美法官驳回美光、三星和 SK 海力士 DRAM 价格操纵案撤诉动议](#item-finance-news-2) ⭐️ 7.0/10
3. [中美俄领导人将在深圳 APEC 场边首次举行三方会晤](#item-finance-news-3) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Meta FAIR 与 NYU 用 200+ 模型拆解多模态视觉编码器](https://www.reddit.com/r/MachineLearning/comments/1xx1k2o/meta_fair_nyu_unbundling_multimodal_vision/) ⭐️ 8.0/10

Meta FAIR 与 NYU 的作者称，他们在相同数据上从零训练 200 多个多模态模型（LLM 本身也从头训练），把标准视觉编码器拆成三项独立选择——单独预训练、仅供视觉 token 使用的参数、放在 LLM 之前——并逐一测试；主对比使用 Qwen3-1.7B 与 4B 骨干、约 0.4B 视觉容量，另设 0.6B 至 6.4B 的缩放阶梯，评测覆盖 Cambrian 的 16 个 448 像素 VQA 基准和 12 个语言基准。结论是编码器预训练可选：用对比学习、自监督和两种 captioning 目标预训练的编码器，在同等总算力下最多与随 LLM 一起从零训练的编码器打平；把 MetaCLIP 预训练延长 6.5 倍虽将 ImageNet 线性探针从 80.4% 提到 84.4%，却没有提升 VQA。视觉专用参数则不可省：无编码器模型在 0.6B 到 6.4B 每一档都落后，需要约 3 倍算力才能追上。位置同样是可选项——“in-fusion” 在 LLM 前 8 层加入零初始化的视觉专用权重（注意力投影与 FFN），文本 token 从不使用它们，在 1.7B 到 6.4B 与编码器方案持平，首 token 时间约低 13%；1.7B 下第 1–8 层的视觉专用分支取得 45.0 VQA（编码器 44.4），文本共享这些参数时为 42.3，放在最后 8 层则只有 35.1。

reddit · r/MachineLearning · /u/trungh98 · 11月15日 17:38

**「背景」** 多模态大模型通常先把图像转成视觉 token，再交给语言模型处理；主流做法是使用预训练的视觉编码器，但近期也出现了让编码器与语言模型一起从零训练、甚至完全去掉独立编码器的方案。该研究把这一标准设计拆成三个可分别检验的选择：是否单独预训练编码器、是否保留仅供视觉 token 使用的参数，以及是否把编码器放在语言模型之前。

**「影响」** 对架构选型来说，可直接操作的结论是：可以省掉编码器的单独预训练预算，但不能省掉视觉专用参数。完全不设编码器的路线要在同等数据上多付出约 3 倍算力，而 in-fusion 在不改动 LLM 文本通路的前提下可换来约 13% 的首 token 延迟改善，代价是前若干层各需额外维护一组视觉专用权重。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://arxiv.org/pdf/2611.17334v1">Unbundling Multimodal Vision Encoding - arXiv.org</a></li>
<li><a href="https://sparsenotes.com/posts/2026/11/papers/unbundling-multimodal-vision-encoding/">Unbundling Multimodal Vision Encoding | Sparse Notes</a></li>

</ul>
</details>

**标签**: `#multimodal LLMs`, `#vision encoders`, `#model architecture`, `#pretraining`, `#research`

---

<a id="item-tech-news-2"></a>
### [美团开放 LongCat-2.5 权重，称训练未用英伟达 GPU](https://the-decoder.com/meituan-releases-a-1-6-trillion-parameter-agent-model-that-never-touched-an-nvidia-gpu/) ⭐️ 8.0/10

美团 LongCat 团队在正式发布一周后公开了 LongCat-2.5 的模型权重；该模型面向能自主完成冗长、多步骤任务（尤其是编程）的智能体，以 MIT 许可证发布并可商用，支持文本、图像和视频输入。官方称其总参数为 1.6T、每个 token 激活约 480 亿参数，训练全程使用华为升腾加速卡，未使用英伟达 GPU。官方给出的 Terminal Bench v2.1 得分为 88.4，略低于 Claude Opus 5 的 89.1；训练硬件说法和这一单项基准成绩均来自发布方，尚待独立验证。

telegram · zaihuapd · 11月15日 11:08

**「前代基础」** LongCat-2.5 是 LongCat-2.0 的后继版本。此前的 LongCat-2.0 已宣称在华为升腾芯片上完成训练和推理服务，使用华为 HCCL 处理超过 30 万亿 token，训练集群包含 5 万颗国产 ASIC，且没有使用英伟达 GPU；该模型以 MIT 许可证开源。因此，LongCat-2.5 的“未使用英伟达 GPU”说法延续了 2.0 已公布的硬件路线。

**「影响」** 对希望商用部署的团队而言，MIT 许可证减少了授权限制，但 1.6T 总参数、每 token 约 48B 激活的模型仍需相应的大规模推理基础设施；在采用前应自行复现基准并评估服务成本。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://aicodingweekly.datadriftpress.com/p/61-longcat-edges-out-gpt-5-5">#61 - LongCat edges out GPT-5.5 | AI Coding Weekly</a></li>
<li><a href="https://wireread.com/news/meituan-longcat-2-open-source">LongCat - 2 .0: first trillion -param model built without Nvidia</a></li>

</ul>
</details>

**标签**: `#large language models`, `#open weights`, `#agentic coding`, `#Huawei Ascend`, `#AI hardware`

---

<a id="item-tech-news-3"></a>
### [MacBook Pro OLED 屏幕的 PWM 频闪问题](https://macanorak.com/the-macbook-pros-oled-pwm-problem-when-a-better-display-becomes-worse-to-use/) ⭐️ 7.0/10

MacAnorak 的文章聚焦 MacBook Pro 的 OLED 屏幕，讨论 PWM 调光频闪为何会让部分对闪烁敏感的用户感到不适，即使这块屏幕在技术上更先进。文章的核心论点是“更好的显示”不一定“更好用”，把硬件规格与个体视觉舒适度区分开来。文中的频闪测量与影响分析仍属于作者和讨论者的判断，并非苹果官方说明或独立临床结论。

hackernews · MacAnorak · 11月15日 13:15 · [社区讨论](https://news.ycombinator.com/item?id=50506719)

**「背景」** PWM 调光是 OLED 屏幕常用的亮度控制方式：屏幕以固定频率快速开关像素，亮度越低，亮灭占空比越小；当频率不够高时，部分敏感用户会感到闪烁、头痛或眼疲劳。苹果在 MacBook Pro 上把 2021 年起使用的 Mini-LED 换成了串联 OLED，并命名为 PROLED XDR，同时继续销售 Mini-LED 机型。Notebookcheck 的评测指出，这块 OLED 的 PWM 频率约为 240 Hz，并认为即使有 DC 调光，敏感用户仍可能受影响；该评测引用的对比显示，Mini-LED 机型约为 14,880 Hz。

**「对闪烁敏感用户的实际影响」** 对闪烁敏感的用户来说，直接后果是 PWM 频率无法在系统设置中调整，购买前只能依赖实机试用或第三方测量来判断能否长期使用；外部对手机 OLED 的测试显示，PWM 频率常落在 60–480 Hz，正好处于敏感人群容易出现症状的区间，而评论中引用的研究称人眼可感知到高于面板刷新率两倍以上的闪烁。需要注意，MacBook Pro 串联 OLED 的等效频率在社区仍有争议：有读者根据示波器波形推断两层以 480 Hz、180 度反相驱动，等效约 960 Hz，这与原文测试者得出的 240 Hz 结论并不一致，具体数值仍有待独立验证。

**「社区讨论」** HN 讨论中，legitronics 质疑文中 240Hz 的测量结论，认为 tandem OLED 可能以 480Hz、180 度反相工作，在大部分可用亮度下形成等效 960Hz；achr2 则引用一篇 Nature 论文称，人可感知超过显示器频率两倍的闪烁。其他评论者把话题扩展到显色指数（CRI）、运动模糊和脑震荡后的屏幕敏感，但这些多为个人经历或观点，并非统一结论。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://macanorak.com/the-macbook-pros-oled-pwm-problem-when-a-better-display-becomes-worse-to-use/">The MacBook Pro ’s OLED PWM Problem: When a ‘Better’ Display...</a></li>
<li><a href="https://www.notebookcheck.net/Amazing-OLED-panel-Apple-MacBook-Pro-14-PROLED-XDR-Review.1438048.0.html">Amazing OLED panel - Apple MacBook Pro ... - Notebookcheck Review</a></li>
<li><a href="https://www.youtube.com/watch?v=sGgowKoztzk">Is the PROLED ( OLED ) MacBook Pro a Disaster? Flicker ... - YouTube</a></li>
<li><a href="https://www.androidcentral.com/phones/what-is-pwm-display-flicker-tips-and-tricks">What is PWM dimming, and what are the alternatives? | Android Central</a></li>
<li><a href="https://trysundown.com/blog/pulse-width-modulation-monitor">PWM Monitor Flicker : Why Your Screen Hurts, and Fixes</a></li>

</ul>
</details>

**标签**: `#OLED PWM`, `#display flicker`, `#MacBook Pro`, `#hardware ergonomics`, `#Hacker News discussion`

---

<a id="item-tech-news-4"></a>
### [Protomaps 自托管地图瓦片的成本与限制](https://bruceroettgers.eu/blog/protomaps/) ⭐️ 7.0/10

一篇技术博文梳理了用 Protomaps 和 PMTiles 自托管地图瓦片的做法，目标读者是希望降低地图成本、减少对商业地图 API 依赖的开发者。文章的核心主张是：基础底图瓦片可以存成静态文件并通过对象存储分发，从而避开按请求计费的商业服务；但这是实践性经验，不是厂商发布的基准测试。评论同时指出，高分辨率卫星影像在高缩放级别下会迅速膨胀到数百 TB，因此“便宜且容易”主要适用于常规底图，而非所有地图数据。

hackernews · bcye · 11月15日 19:26 · [社区讨论](https://news.ycombinator.com/item?id=50509837)

**「背景：地图瓦片与 PMTiles」** 地图瓦片是把可平移、缩放的地图切成 256 或 512 像素见方的块，常用 MBTiles 或 PMTiles 归档。Protomaps 提供可免费定制、能以单个静态文件部署在云存储上的世界地图；这种“无服务器”瓦片形态是理解其自托管成本与部署门槛的前提。

**「影响」** 对独立开发者和小型项目来说，这种模式把地图底图变成可自行托管、按存储和流量计费的基础设施，便于控制隐私与访问权限；代价是要自己处理瓦片生成、存储和分发，卫星影像等高缩放数据会显著抬高存储成本。

**「社区讨论」** 评论中，boramalper 推荐了无需注册和 API key 的 OpenFreeMap，neomantra 分享了在 Cloudflare R2 后托管 PMTiles 以掌握隐私和访问控制的部署方式，thatslast 则表示 Protomaps 让一个 Wikipedia 步行游戏副项目变得可负担。motoroco 提醒，高分辨率卫星影像到 z17 时存储就会变得很大，全球高分辨率覆盖可能达到数百 TB；这些是社区经验，不是独立基准。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://protomaps.com/">Protomaps - The open source map in a file</a></li>
<li><a href="https://chrisamico.com/blog/2024-02-13/self-hosted-maps/">How to make self - hosted maps that work everywhere and cost next...</a></li>
<li><a href="https://github.com/Rezivure/Grid-Protomaps">Rezivure/Grid- Protomaps : The Protomaps &quot;serverless&quot; map tile ...</a></li>

</ul>
</details>

**标签**: `#Protomaps`, `#PMTiles`, `#self-hosting`, `#maps`, `#open source`

---

<a id="item-tech-news-5"></a>
### [Raschka 解析现代大语言模型的位置嵌入](https://magazine.sebastianraschka.com/p/understanding-positional-embeddings) ⭐️ 7.0/10

Sebastian Raschka 发表了一篇关于现代大语言模型位置嵌入的技术解析文章，讨论集中在实现层面。文章在 Hacker News 上引发争论：有评论者认为，仅理解实现不足以真正掌握位置嵌入。该评论者主张位置嵌入属于群表示，并举例称旋转位置嵌入是平移群的表示。

hackernews · vismit2000 · 11月15日 12:14 · [社区讨论](https://news.ycombinator.com/item?id=50506376)

**「背景」** Transformer 的自注意力机制本身对 token 的排列顺序不敏感，因此必须显式注入位置信息，否则改变词序不会影响模型输出。GPT-2 采用的做法是把可学习的位置向量加到 token embedding 上，属于绝对位置编码，并绑定其原始的 1,024 上下文长度。Raschka 于 2026 年 11 月 15 日发布的这篇 Ahead of AI 文章从这类经典方法讲到 RoPE、部分 RoPE 与 NoPE，并附带一个小型 PyTorch 实现以及对 2025—2026 年开放权重模型所用方案的梳理。

**「社区讨论」** 评论者 programjames 认为，文章偏重实现而缺少理论根基；其核心论点是位置嵌入可被视为群表示，旋转位置嵌入对应平移群，且 n 维平移群 ℝⁿ 是阿贝尔群。该观点属于评论者个人论述，不代表文章已给出相同结论。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://magazine.sebastianraschka.com/p/understanding-positional-embeddings">Understanding Positional Embeddings in Modern LLMs</a></li>
<li><a href="https://daily.dev/posts/understanding-positional-embeddings-in-modern-llms-415mglzuo">Understanding Positional Embeddings in Modern LLMs</a></li>
<li><a href="https://sebastianraschka.com/blog/">Blog and Notes - Sebastian Raschka, PhD Positional embeddings in modern LLMs: from GPT-2 to RoPE and ... RoPE vs NoPE: Modern LLM Position Encoding (2026 ... Ahead of AI | Sebastian Raschka, PhD | Substack Sebastian Raschka Explains Positional Embeddings… · AGI Hunt</a></li>

</ul>
</details>

**标签**: `#positional embeddings`, `#large language models`, `#transformer architecture`, `#deep learning`, `#technical explainer`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [CNBC：卢特尼克因英伟达持股与融资关系面临伦理质疑](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 8.0/10

CNBC 11 月 13 日报道，美国商务部长霍华德·卢特尼克因其子领导的坎托·菲茨杰拉德在 2025 年 9 月至 2026 年 3 月间将申报的英伟达持股数量减少近 50%、同时继续参与英伟达合作伙伴融资而面临伦理质疑。Axios 报道称，卢特尼克曾抵制对涉嫌将英伟达先进 AI 芯片输往中国的 Megaspeed 采取行动，尽管特朗普已于 11 月 5 日第三次授权对这类公司实施新出口限制；英伟达 CEO 黄仁勋周四辞职。

rss · CNBC Finance · 11月15日 19:58

**「背景」** 卢特尼克于 2025 年 2 月离开坎托·菲茨杰拉德出任商务部长，该公司现由其子布兰登和凯尔领导；证券文件显示，英伟达曾是该券商第二大申报持股。

**「影响」** 美国政府部门间出现公开分歧：财政部长贝森特称，财政部、国防部、国务院和美国贸易代表办公室都支持将 Megaspeed 列入实体清单（限制企业名单）已有数月，而负责该清单的商务部被追问内部流程。

**标签**: `#Nvidia`, `#U.S. export controls`, `#Cantor Fitzgerald`, `#Howard Lutnick`, `#conflict of interest`

---

<a id="item-finance-news-2"></a>
### [美法官驳回美光、三星和 SK 海力士 DRAM 价格操纵案撤诉动议](https://www.tomshardware.com/tech-industry/big-tech/judge-denies-motion-to-dismiss-dram-price-fixing-lawsuit-against-micron-samsung-and-sk-hynix-says-chipmakers-acted-like-hawks-flying-in-formation-finds-evidence-of-dram-collusion-plausible-after-500-percent-price-surge) ⭐️ 7.0/10

美国法官 Noël Wise 驳回美光、三星和 SK 海力士要求撤销 DRAM 价格操纵集体诉讼的动议，案件可继续审理。原告为 17 名个人和小企业，他们指控这三家公司在一年内四次同步限制 DRAM 供应，使价格最高上涨 500%；法院认为这些证据足以让案件推进，但共谋尚未被判定。

telegram · zaihuapd · 11月15日 16:39

**「背景」** 这起拟议集体诉讼由 17 名个人和小企业提起，指控三家存储芯片商在一年内四次同步限制 DRAM 供应、推高价格；撤诉动议是请求法院在开庭审理前直接驳回案件，而法官认为现有证据足以让诉讼继续。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.tomshardware.com/tech-industry/big-tech/judge-denies-motion-to-dismiss-dram-price-fixing-lawsuit-against-micron-samsung-and-sk-hynix-says-chipmakers-acted-like-hawks-flying-in-formation-finds-evidence-of-dram-collusion-plausible-after-500-percent-price-surge">Judge denies motion to dismiss DRAM price - fixing lawsuit against...</a></li>
<li><a href="https://www.techpowerup.com/354863/samsung-sk-hynix-and-micron-fail-to-get-dram-antitrust-suit-dismissed">Samsung , SK hynix , and Micron Fail to Get DRAM Antitrust Suit ...</a></li>

</ul>
</details>

**标签**: `#DRAM`, `#antitrust`, `#price-fixing`, `#Micron`, `#Samsung`

---

<a id="item-finance-news-3"></a>
### [中美俄领导人将在深圳 APEC 场边首次举行三方会晤](https://apnews.com/article/trump-xi-putin-summit-china-5fe92253ef38100bae913834a9b74d72) ⭐️ 7.0/10

中国外交部发言人宣布，中美俄三国领导人计划于 11 月 19 日在深圳 APEC 峰会期间举行三方会晤；会晤在 APEC 场边举行，不属于正式议程，媒体称这将是三国领导人首次专门举行三方会晤。目前尚无议程或成果信息。

telegram · zaihuapd · 11月16日 01:38

**「背景」** 亚太经合组织（APEC）2026 年峰会由中国在深圳主办，领导人会议定于 11 月 18 日至 19 日举行；这是中国继 2001 年和 2014 年后第三次主办该峰会。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/APEC_China_2026">APEC China 2026 - Wikipedia</a></li>
<li><a href="https://www.gessymorgan.com/apec-2026-china/">APEC 2026 China: Shenzhen Summit Dates and Agenda</a></li>

</ul>
</details>

**标签**: `#China-US-Russia relations`, `#APEC summit`, `#geopolitics`, `#diplomatic meeting`

---