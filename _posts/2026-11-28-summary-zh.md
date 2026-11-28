---
layout: default
title: "Horizon Summary: 2026-11-28 (ZH)"
date: 2026-11-28
lang: zh
---

> 从 31 条内容中筛选出 14 条重要资讯。

---

**科技新闻**
1. [OpenSec 披露 Linux nfsd 9.8 分预认证漏洞](#item-tech-news-1) ⭐️ 8.0/10
2. [Google DeepCrossAttention 宣称质量相当且最高提速 3 倍](#item-tech-news-2) ⭐️ 7.0/10
3. [计算机检查的证明仍可能为假](#item-tech-news-3) ⭐️ 7.0/10
4. [多州总检察长起诉 SpaceX，指 Grok 生成儿童性虐待图像](#item-tech-news-4) ⭐️ 7.0/10
5. [WebRTC 信用卡窃取脚本被指现身热门购物网站](#item-tech-news-5) ⭐️ 7.0/10
6. [SemiAnalysis 实测 Trainium3 推理性能与微架构](#item-tech-news-6) ⭐️ 7.0/10
7. [《我的世界》基岩版资源包漏洞影响 26.52 至 26.63，26.65 修复](#item-tech-news-7) ⭐️ 7.0/10
8. [微软推进 Windows 内置驱动替代第三方驱动](#item-tech-news-8) ⭐️ 7.0/10
9. [Convex 编码 skill 被指上传用户应用想法](#item-tech-news-9) ⭐️ 6.0/10
10. [Michael Nielsen 下线《Neural Networks and Deep Learning》](#item-tech-news-10) ⭐️ 6.0/10
11. [黑客用 AI 工具 Artex 攻击 CIA 等美情报机构](#item-tech-news-11) ⭐️ 6.0/10

**财经新闻**
1. [国常会部署完善资本市场稳市机制](#item-finance-news-1) ⭐️ 8.0/10
2. [蜜雪冰城 5 亿元参与 DeepSeek 第二轮融资，本轮规模约千亿元](#item-finance-news-2) ⭐️ 7.0/10
3. [央行发布大额存单新规 个人起购门槛降至 10 万元](#item-finance-news-3) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [OpenSec 披露 Linux nfsd 9.8 分预认证漏洞](https://opensec.in/blog/nfs2root-cve-2026-99362) ⭐️ 8.0/10

OpenSec 披露 Linux 内核 NFS 服务器 nfsd 中的预认证堆溢出漏洞 CVE-2026-99362，CVSS 评分为 9.8。据该披露，攻击者无需登录，只需向 tcp/2049 发送一条连接，即可越界写入内核堆并取得 root shell。该漏洞自 2014 年的 Linux 3.16 起存在，影响启用 NFSv4.1 或 4.2 的主机，包括文件服务器、NAS 和集群存储节点。修复已在 6.12.117、6.18.61、7.3.2 和 7.4-rc1 发布，需升级内核并重启；无法立即升级的环境可通过防火墙限制 tcp/2049 访问。CVE 于 2026 年 11 月 20 日公开。

telegram · zaihuapd · 11月27日 12:57

**「背景」** nfsd 是 Linux 内核中的 NFS 服务器端实现，NFS 用于在网络上共享文件系统；当主机在 tcp/2049 上对外提供 NFSv4.1/4.2 服务时，这些请求会进入内核的 nfsd 代码路径。所谓“预认证”意味着攻击者不必先完成 NFS 登录或取得凭据，只要能连接到该端口，就能在认证之前触发漏洞。

**「受影响方的处置与代价」** 对运行 NFSv4.1/4.2 的文件服务器、NAS 和集群存储节点来说，现实选择只有两条：升级到 6.12.117、6.18.61、7.3.2 或 7.4-rc1 并重启，或把 tcp/2049 收紧到可信客户端。后者正是 NFS 服务的入口，限制该端口会同时切断合法客户端的挂载访问（外部报道也把“限制对 TCP 2049 的访问”列为临时缓解手段）。源报道只列出上述几条内核分支的修复版本，未说明其他长期支持分支是否同样获得回补，使用这些内核的部署需先向发行版确认。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://opensec.in/blog/nfs2root-cve-2026-99362">NFS2ROOT ( CVE - 2026 - 99362 ): pre-auth root in Linux nfsd | OpenSec</a></li>
<li><a href="https://www.getpagespeed.com/server-setup/security/nfs2root-cve-2026-99362-centos-7">NFS2ROOT ( CVE - 2026 - 99362 ) on CentOS 7: Fixed Kernel</a></li>
<li>Linux users beware — a 12-year-old bug could let hackers gain access ...</li>

</ul>
</details>

**标签**: `#Linux kernel`, `#NFS`, `#CVE`, `#security vulnerability`, `#pre-auth RCE`

---

<a id="item-tech-news-2"></a>
### [Google DeepCrossAttention 宣称质量相当且最高提速 3 倍](https://research.google/blog/supercharging-transformer-residual-connections/) ⭐️ 7.0/10

Google Research 的一篇博客介绍了 DeepCrossAttention，这是一种用于 Transformer 残差连接与注意力的方法，声称在模型质量相当的情况下最高可实现 3 倍加速。现有材料没有给出具体基准、模型规模、硬件条件或独立复现结果，因此“3 倍”仍是研究团队的宣称，而非已独立验证的性能结论。该方法的可用性、代码发布情况和兼容范围也未在提供的信息中说明。

hackernews · ComputedCamp995 · 11月27日 23:06 · [社区讨论](https://news.ycombinator.com/item?id=50672565)

**「背景」** Transformer 的残差连接把各层输出逐层相加，让信息在深层网络中流动，但相关论文指出这种结构会出现信息稀释。DeepCrossAttention（DCA）用可学习权重进行跨层路由来组合信息，Google Research 的博客则以标准顺序残差连接与 DCA 的对比来说明这一改动。

**「对开发者的影响」** 若要采用 DCA，改动落在每个解码器块：需在自注意力之外加入三个独立的 GRN 实例，而不是只调整训练配置或超参数。该改造只适用于 Transformer 解码器；非 Transformer 的 ResNet 类模型只能参考其更一般的残差连接泛化。论文称 DCA 在语言建模基准上优于 LAuReL、DenseFormer 和 Hyper-Connections，但当前材料未提供独立复现结果。

**「社区讨论」** 有评论者批评博客用折线连接不同方法缺乏时间关系，认为应改用柱状图；另一位评论者则提出该方法是否与 DenseNet 的思路相似。这些讨论针对呈现方式和概念类比，并未提供独立的速度或质量验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://research.google/blog/supercharging-transformer-residual-connections/">Supercharging transformer residual connections</a></li>
<li><a href="https://arxiv.org/html/2502.06785v1">DeepCrossAttention : Supercharging Transformer Residual ...</a></li>
<li><a href="https://arxiv.org/html/2502.06785">DeepCrossAttention : Supercharging Transformer Residual Connections</a></li>
<li><a href="https://www.alphaxiv.org/overview/2502.06785v1">DeepCrossAttention : Supercharging Transformer Residual... | alphaXiv</a></li>
<li><a href="https://openreview.net/pdf?id=j3JBfFnGYh">DeepCrossAttention : Supercharging Transformer Residual Connections</a></li>

</ul>
</details>

**标签**: `#transformers`, `#model efficiency`, `#attention mechanisms`, `#Google Research`, `#AI research`

---

<a id="item-tech-news-3"></a>
### [计算机检查的证明仍可能为假](https://cr.yp.to/proofs/falseccp.html) ⭐️ 7.0/10

一篇短文主张，“计算机检查过的证明”不能自动等同于真证明：如果证明检查器本身存在健全性（soundness）缺陷，它就可能接受错误证明；文章因此把独立验证器视为主要缓解手段，而不是把一次检查通过当作最终保证。该文是论证性文章，重点在论证与缓解思路。评论中提到的具体案例包括：一名 DeepMind 研究者构造的“证明”分别利用 Lean 和一个当时发布仅一周的 nanoda 版本中的不同缺陷，通过了这两个检查器。

hackernews · \_tk\_ · 11月27日 15:26 · [社区讨论](https://news.ycombinator.com/item?id=50667989)

**「背景」** 计算机检查证明是由软件逐条核对形式化推导，而不是靠人通读全部论证，因此检查器本身是否可靠，直接决定“证明已通过检查”这一结论有多强。cr.yp.to 的这篇文章讨论的正是这一类风险：一些声称为证明的每一步把关的程序，已被报告存在 soundness bug，可能让虚假陈述通过检查。

**「影响」** 对依赖形式化验证的团队，这意味着验收流程要把“检查器接受了证明”与“证明目标确实为真”分开；在高保证场景中，不能仅凭单一检查器通过就排除检查器自身缺陷，应采用多个独立实现的验证器或补充人工审阅。

**「社区讨论」** 评论者不否认健全性缺陷存在，但 twotwotwo 和 dwheeler 认为文章低估了多检查器门槛：要误导数学界，需同时骗过多个独立检查器，且证明在非形式审阅下不显得可疑；dwheeler 还称 Metamath 的 set.mm 和 iset.mm 要求通过 5 个独立实现、5 种语言的验证器。gr\_norm 则认为这类缺陷数十年来少到几乎可以写进一条推文，对绝大多数软件已足够。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://cr.yp.to/proofs/falseccp.html">False computer - checked proofs (djb)</a></li>

</ul>
</details>

**标签**: `#formal-verification`, `#proof-assistants`, `#soundness-bugs`, `#software-correctness`, `#Lean`

---

<a id="item-tech-news-4"></a>
### [多州总检察长起诉 SpaceX，指 Grok 生成儿童性虐待图像](https://www.oag.state.va.us/media-center/news-releases/jay-jones/3162-attorneys-general-jones-and-rayfield-file-suit-against-spacex-parent-company-of-x-xai-and-grok-over-creation-and-promotion-of-child-exploitation-and-non-consensual-images-on-platform) ⭐️ 7.0/10

弗吉尼亚州总检察长办公室称，琼斯（Jay Jones）与雷菲尔德（Rayfield）两名州总检察长已起诉 SpaceX，要求阻止 Grok 生成儿童性虐待材料和未经同意的私密图像。诉方将 SpaceX 列为 X 和 xAI 的母公司，并寻求让平台运营方对 Grok 的模型输出承担责任。上述指控尚未经法院认定，目前也没有法院裁决。

hackernews · DeepLogin · 11月27日 19:42 · [社区讨论](https://news.ycombinator.com/item?id=50670855)

**「背景」** 《卫报》2026 年 9 月报道的一起诉讼中，一名童年性虐待幸存者起诉 xAI，指控 Grok 利用她受虐的照片生成了新的非法色情图像。此次州总检察长把 SpaceX 作为 xAI 的母公司列为被告，使同一类 Grok 生成内容的争议从个人提起的侵权诉讼扩展到州层面的法律行动。

**「社区讨论」** 评论区有人困惑：此类内容既然已在各平台被禁，Grok 是默认设置过于宽松，还是用户需要刻意绕过限制；也有人追问制作和传播者本人的责任。另一名评论者声称，美国最高法院已裁定仅用于个人消费的 AI 生成儿童性虐待材料受言论保护，但涉及真实儿童的刻画不受保护，并对报复色情是否适用表示不确定——这属于评论者的法律判断，并非本案已确认的结论。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.theguardian.com/technology/2026/sep/03/elon-musk-ai-grok-child-porn-lawsuit">Child sexual abuse survivor alleges Elon Musk’s AI... | The Guardian</a></li>

</ul>
</details>

**标签**: `#AI safety`, `#generative AI`, `#content moderation`, `#AI regulation`, `#xAI/Grok`

---

<a id="item-tech-news-5"></a>
### [WebRTC 信用卡窃取脚本被指现身热门购物网站](https://www.infohawk.com/news/2026-11-27-black-friday-webrtc-skimmer) ⭐️ 7.0/10

据 Infohawk 报道，一些热门购物网站被指存在利用 WebRTC 的信用卡信息窃取脚本；报道发布于 2026 年 11 月 27 日。现有信息只说明脚本“被发现”且使用 WebRTC，未披露受影响网站数量、脚本加载方式或是否已造成实际支付数据泄露。报道将风险指向电商页面中的第三方脚本，这使在这些站点结账的消费者面临潜在的数据窃取风险。

hackernews · scanr · 11月27日 15:40 · [社区讨论](https://news.ycombinator.com/item?id=50668145)

**「背景」** WebRTC 是浏览器内置的实时通信接口，通常用于音视频通话和点对点数据传输。信用卡盗刷脚本（skimmer）则是在电商结账页面偷偷收集表单数据的恶意 JavaScript，常通过第三方脚本或供应链注入进入站点。

**「影响与应对」** 对电商站点而言，直接后果是：结账页上任何被攻破的第三方脚本都可能读取并外传支付数据，而 WebRTC 只是较少被监控的通道；评论者 afavour 指出，同样的窃取用普通 HTTP 请求也能完成。运维团队因此应把第三方脚本清单、CSP 限制和结账页异常外联监控作为主要控制点，而不是只封禁 WebRTC；本月 Optimizely 平台被植入恶意 JavaScript、波及 178 家组织的事件表明，这类供应链入口已被实际利用。

**「社区讨论」** 评论者多将问题归因于第三方脚本：afavour 认为关键不在 WebRTC 本身，而在于它较少被监控、移动端更难检测，简单 HTTP 请求也能实现同样目的，网站只要嵌入第三方脚本就始终有风险；jszymborski 则以此支持继续使用广告拦截。另有评论提出更激进的方案，包括不允许网站执行任意代码、让广告在无 JavaScript 的沙箱中渲染，以及用非对称密码学替代支付中的对称密钥。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://cybersecuritynews.com/optimizely-websites-hijacked/">Hackers Infect 178 Major Websites via Optimizely to Steal Credit ...</a></li>

</ul>
</details>

**标签**: `#web security`, `#credit card skimming`, `#WebRTC`, `#third-party scripts`, `#e-commerce`

---

<a id="item-tech-news-6"></a>
### [SemiAnalysis 实测 Trainium3 推理性能与微架构](https://newsletter.semianalysis.com/p/trainium3-inferencex) ⭐️ 7.0/10

SemiAnalysis 将 AWS Trainium3 纳入其开源 InferenceX/UBenchX 基准，并通过 AgentX 回放真实编码 agent 会话进行端到端推理测试；该机构称，Trainium3 PDS + vLLM 在 TCO 对 p90 交互性曲线上，除 Nvidia Vera Rubin 外优于其他加速器，在 TCO 口径的 token 生成成本上与 GB300 互有胜负、部分场景更优。文章称其优势不只来自亚马逊的低成本供应链，也来自微架构：Trainium 的 Descriptor Generation Engines（DGE）对应 Nvidia TMA 和 AMD MI455X TDM，微基准显示其能在较小消息尺寸下达到峰值 HBM 带宽利用率，而 Nvidia GPU 无法做到。测试还覆盖 SBUF 到 PSUM 的周期级 SRAM 延迟与带宽、机架级带宽和延迟、attention 指数运算，以及不同 head\_dim 对 roofline 占比的影响；这些是 SemiAnalysis 的基准结果，并非 AWS 官方发布。

rss · Semianalysis · 11月27日 15:54

**「背景」** Trainium 是 AWS 自研的 AI 加速器系列，其架构把瓦片（tile）作为一等公民、从底层面向机器学习负载设计，而 Nvidia 的数据中心 GPU 源自图形渲染管线，逐代加装 Tensor Core、TMA 等 AI 专用单元。据 Idlen 报道，2026 年 4 月亚马逊宣布向 Anthropic 追加最高 250 亿美元投资，并承诺 1000 亿美元的 AWS Trainium/Graviton 投入，为 Claude 锁定 5 GW 算力，这使 Trainium3 的推理性价比成为需要独立基准验证的议题。

**「推理成本与选型影响」** 对运行智能体推理的团队来说，Trainium3 搭配 PDS 与 vLLM 已进入按 token 成本选型的候选范围：SemiAnalysis 的 TCO 对 p90 交互性曲线显示，它仅次于 Vera Rubin，优于其他加速器。计划扩容推理集群的团队可将其纳入每美元性能比较，但迁移前需用自身模型验证 vLLM、量化格式与 AWS Neuron 软件栈的兼容性，因为该结论来自特定智能体会话回放和基准测试，并非对所有负载的保证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.idlen.io/news/amazon-anthropic-25-billion-investment-100-billion-aws-trainium-april-2026/">Amazon Pours Another $25B Into Anthropic — $100B AWS Trainium ...</a></li>
<li><a href="https://nitter.rdrama.net/ArtificialAnlys/status/2110903253013762365">Artificial Analysis (@ArtificialAnlys): &quot;Initial results for NVIDIA &#x27;s Vera ...</a></li>

</ul>
</details>

**标签**: `#AWS Trainium`, `#AI hardware`, `#inference`, `#microarchitecture`, `#Nvidia`

---

<a id="item-tech-news-7"></a>
### [《我的世界》基岩版资源包漏洞影响 26.52 至 26.63，26.65 修复](https://www.zaikei.co.jp/article/20261119/878386.html) ⭐️ 7.0/10

附加组件开发者 8Crafter 于 11 月 15 日公开，《我的世界》基岩版资源包若包含 content.zipe，可改动 Ore UI 界面框架文件并运行隐藏脚本；其称已确认影响 26.52 至 26.63，更早版本也可能受影响，覆盖 PC、手机和主机，Java 版不受影响。玩家加入服务器或 Realm 并开启资源包自动下载时，可能无需手动安装就收到问题文件。已列出的利用方式包括删除全部存档、获取玩家 IP，以及在 Windows 特定条件下无提示打开任意 URI、启动资源包内批处理文件下载恶意软件。Mojang 已在 26.65 版修复；AxmBro 发布的 Windows 只读检测工具可查找 content.zipe，但不能判定资源包是否恶意。

telegram · zaihuapd · 11月27日 18:04

**「背景」** 基岩版允许服务器或 Realm 向客户端推送资源包；当自动下载开启时，玩家加入后便会加载包内内容。此次漏洞正是利用这一加载路径，使带有 content.zipe 的资源包能够改动 Ore UI 框架文件并运行隐藏脚本。

**「影响」** 仍使用 26.52 至 26.63 的基岩版玩家应升级到 26.65；在修复前，加入开启资源包自动下载的服务器或 Realm 时，玩家可能无需手动安装就收到恶意包，导致存档被删除、IP 泄露，Windows 上还可能触发任意 URI 或下载恶意软件。AxmBro 的检测工具只能查找 content.zipe，不能判断资源包是否恶意，因此不能替代升级。

**标签**: `#Minecraft Bedrock`, `#resource pack vulnerability`, `#security`, `#Ore UI`, `#malware`

---

<a id="item-tech-news-8"></a>
### [微软推进 Windows 内置驱动替代第三方驱动](https://www.techspot.com/news/114721-microsoft-wants-replace-most-third-party-device-drivers.html) ⭐️ 7.0/10

微软在 Ignite 2026 上确认，正为打印、音频、USB 以太网和摄像头等整类硬件开发 Windows 内置驱动，以减少进入内核的第三方代码。打印机是首批重点，近期推出的 Windows Ready Print 模式用于替代旧式第三方打印驱动。Windows 产品经理 Mehmet Kucukgoz 表示，SoundWire、SDCA 等音频类驱动将很快成为 Windows 内置组件，I3C 总线、USB 以太网和 MIPI 摄像头类驱动仍在开发中。微软近期还推出驱动质量倡议（DQI），鼓励第三方开发者和 OEM 尽量采用内置驱动并提高可靠性、质量和安全标准；部分第三方驱动被取代仍属未来工作。

telegram · zaihuapd · 11月28日 02:09

**「背景」** Windows Ready Print 是这一思路的首个落地场景：它优先使用基于 IPP 的 Windows 内置打印驱动。据 Windows Forum 汇总，从 2026 年 7 月起，受支持的新打印机安装将优先采用该模式，这使打印成为微软用内置组件替代部分第三方驱动的首个具体类别。

**「影响」** 对打印机、音频等外设厂商和 OEM 而言，适配重点将转向 Windows 内置类驱动与 DQI 标准，定制内核驱动的空间可能收窄；打印机已因 Ready Print 先受影响，其他类别则取决于相关驱动开发进度。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://windowsforum.com/threads/windows-ready-print-in-july-2026-ipp-inbox-printing-policy-controls-protected-mode.425059/">Windows Ready Print in July 2026 : IPP Inbox ... | Windows Forum</a></li>

</ul>
</details>

**标签**: `#Windows`, `#device drivers`, `#Microsoft`, `#kernel security`, `#hardware support`

---

<a id="item-tech-news-9"></a>
### [Convex 编码 skill 被指上传用户应用想法](https://github.com/convex/convex-backend-skill/issues/64) ⭐️ 6.0/10

一项针对 Convex 编码 skill 的 GitHub issue 指控，该工具会把用户的应用想法发送到远程服务器，却没有向用户披露。Convex CEO Jamie 在评论中回应称，插件中的提示词上传用于支撑 Convex 的“quickstart”功能，并说明该功能是已关闭的端到端 vibe-coding 产品 Convex Chef 的后续。争议因此集中在提示词上传的告知与透明度，而非已经独立验证的泄露事件。

hackernews · MickyTheMouse · 11月27日 18:02 · [社区讨论](https://news.ycombinator.com/item?id=50669765)

**「背景」** Convex 此前推出过 AI 应用生成器 Convex Chef，官方将其描述为基于 Convex 的 API 与数据库来生成完整前后端应用的工具。Convex CEO 在讨论中称 Chef 最近已被关闭，而涉事插件中的提示上传用于支撑其“精神继任者”quickstart 功能；当前争议正围绕这一继任功能如何处理用户输入展开。

**「影响」** 对使用该技能的开发者来说，运行技能就可能把应用构想发送到 Convex 的服务器；Convex CEO 已说明，这一上传用于驱动“quickstart”功能。若不接受这种做法，开发者应在使用前检查技能发出的网络请求，或禁用相关上传，并要求维护者明确披露数据流向。

**「社区讨论」** 评论者围绕对厂商与 AI 工具的信任展开争论：有人认为长期看应转向自托管开放权重模型，也有人指出提示注入比模型自主发起恶意工具调用更常见，但并未认定本次上传属于恶意行为。这些意见反映的是对披露和可控性的关注，并不构成对指控事实的独立确认。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://chef.convex.dev/">chef . convex .dev</a></li>
<li><a href="https://github.com/convex/chef">GitHub - convex / chef : The only AI app builder that knows backend</a></li>

</ul>
</details>

**标签**: `#privacy`, `#AI developer tooling`, `#prompt upload`, `#vendor transparency`, `#security`

---

<a id="item-tech-news-10"></a>
### [Michael Nielsen 下线《Neural Networks and Deep Learning》](https://neuralnetworksanddeeplearning.com/) ⭐️ 6.0/10

Michael Nielsen 已将其广受欢迎的免费在线书《Neural Networks and Deep Learning》从原网站下线。现有材料没有给出 Nielsen 的公开理由，也未说明这是永久撤下还是临时移除；对读者和课程使用者而言，最直接的变化是这一免费入口不再可用。Hacker News 的讨论随即把焦点放在此举是否属于针对 AI 风险的抗议，以及撤下此类教材是否会削弱公众理解大型 AI 公司技术的能力。

hackernews · brandonb · 11月27日 19:31 · [社区讨论](https://news.ycombinator.com/item?id=50670757)

**「背景：这本在线教材是什么」** 《Neural Networks and Deep Learning》是 Michael Nielsen 编写的免费在线书，以 neuralnetworksanddeeplearning.com 为官方入口，讲解神经网络与深度学习的核心概念；可检索到的页面版本标注为 2019 年 12 月。该书此前也有 PDF 版本在第三方网站流传，因此此次变化直接影响的是官方在线阅读入口，而非该书内容从未公开过。

**「对读者的实际影响」** 对学习者的实际影响有限：这本原本免费在线的书已被广泛复制和镜像，评论区也有人贴出 web.archive.org 的存档链接，因此下线更像是一种象征性抗议，而不是真正切断获取渠道。原先把官方网址当作入口的读者，则需要改用存档或其他副本，无法再从作者维护的原始页面获取这本书。

**「社区讨论」** 有评论者认为这是失策，主张让外部人士理解大公司闭门开发的技术有助于应对后果；也有人认为这更像一种抗议而非实际措施，并称该书已广泛流传，撤下反而可能增加需求。另有评论把话题引向资本对前沿实验室的推动，以及是否已经实现 ASI 的争论。

<details><summary>参考链接</summary>
<ul>
<li><a href="http://neuralnetworksanddeeplearning.com/">Neural networks and deep learning</a></li>
<li><a href="https://jingyuexing.github.io/Ebook/Machine_Learning/Neural+Networks+and+Deep+Learning-eng.pdf">1 Neural networks and deep learning .pdf</a></li>
<li><a href="http://neuralnetworksanddeeplearning.com/">Neural networks and deep learning</a></li>

</ul>
</details>

**标签**: `#AI safety`, `#neural networks`, `#open educational resources`, `#tech community`, `#AI industry`

---

<a id="item-tech-news-11"></a>
### [黑客用 AI 工具 Artex 攻击 CIA 等美情报机构](https://www.forbes.com/sites/the-wiretap/2026/11/25/us-government-under-ai-cyberattack) ⭐️ 6.0/10

据《纽约时报》报道、经一则 Telegram 帖子转述，黑客攻击了美国中央情报局、国家地理空间情报局和国家情报总监办公室，并使用名为 Artex 的 AI 工具辅助；报道称此次攻击看起来不算严重，受影响的是非机密侦察数据。Artex 可整合多个开源 AI 模型来测试网络和计算机防御，一名中国开发者今年早些时候发布了它，后来将其从自己的 GitHub 账号删除。报道还说，该工具此后被用于多起攻击，包括针对欧盟的一起；FBI 今年早些时候曾警告网络罪犯和间谍正在广泛使用 Artex。上述细节来自媒体转述，所给材料未提供独立验证，也未提供攻击规模、具体时间等更多技术信息。

telegram · zaihuapd · 11月27日 10:42

**「背景」** Artex 是一款由一名中国开发者今年早些时候发布的 AI 渗透测试框架；据 TechCrunch 和 The Record 报道，它可整合 Anthropic Claude、OpenAI GPT 以及 DeepSeek、GLM 等多种模型，用来探测和攻击网络与计算机防御。相关攻击发生后，开发者已将其转为闭源并删除 GitHub 仓库，但 FBI 警告称早先的开源版本仍在流传且“广泛可获取”，并已被用于包括 ConnectWise 供应链攻击在内的多起事件。

**「影响」** 对美国情报机构而言，具体后果是部分非机密侦察数据暴露，而非机密系统被攻破；FBI 此前已警告 Artex 正被网络罪犯和间谍广泛使用，因此防守方也需要把“组合多个开源模型进行网络探测”的行为纳入监测，而不只依赖对单个模型或恶意软件样本的拦截。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://techcrunch.com/2026/11/16/fbi-says-artex-ai-open-source-hacking-tool-used-to-breach-networks-in-under-three-hours/">FBI says Artex AI open source hacking tool used to... | TechCrunch</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/fbi-warns-artex-ai-hacking-tool-is-powering-global-cyberattacks/">FBI warns ARTEX AI hacking tool is powering global cyberattacks</a></li>
<li><a href="https://therecord.media/artex-ai-tool-fbi-flash-alert">FBI flash alert says Artex tool automating cyberattacks at ‘machine...</a></li>
<li><a href="https://rurtnews.com/news/649360-nyt-cia-artex-hack/">CIA , other US spy agencies hit by new hack – NYT — RT World News</a></li>
<li><a href="https://www.forbes.com/sites/the-wiretap/2026/11/25/us-government-under-ai-cyberattack/">The US Government Is Under AI Cyberattack</a></li>

</ul>
</details>

**标签**: `#AI cybersecurity`, `#cyberattacks`, `#open-source AI`, `#threat intelligence`, `#US government`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [国常会部署完善资本市场稳市机制](https://www.tmtpost.com/nictation/8220182.html) ⭐️ 8.0/10

国务院总理李强 11 月 27 日主持召开国务院常务会议，提出持续完善资本市场稳市机制，加力发挥“国家队”稳市作用、进一步优化中央汇金公司的类“平准基金”功能，并完善保险、企业年金、社保基金等中长期资金入市支持引导政策；会议未公布具体规模、工具细节或实施时间表。

telegram · zaihuapd · 11月27日 05:35

**「背景」** “国家队”指以中央汇金公司为代表的国有资金，中央汇金是国有资本投资机构；“平准基金”则是通过在市场下跌时买入、过热时卖出来平抑波动的资金安排。有财经媒体称，这是国常会“再次”就稳市重磅定调（tool-1-3）。

**「影响」** 若上述要求落实，将直接影响上市公司的分红回购安排，以及保险、年金、社保等长期资金的权益配置节奏。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://news.qq.com/rain/a/20261127A09NI000">国 常 会 再次重磅定调 稳 市 ，A股午后全线飙涨_腾讯新闻</a></li>

</ul>
</details>

**标签**: `#中国资本市场`, `#国务院常务会议`, `#中央汇金`, `#平准基金`, `#中长期资金`

---

<a id="item-finance-news-2"></a>
### [蜜雪冰城 5 亿元参与 DeepSeek 第二轮融资，本轮规模约千亿元](https://m.sohu.com/a/1107027659_115479) ⭐️ 7.0/10

据搜狐报道，DeepSeek 已完成第二轮融资，募资规模在 1000 亿至 1055 亿元人民币之间，投后估值约 6155 亿元，新增 31 家出资人，腾讯、宁德时代、中国移动和 vivo 均在列。蜜雪冰城股份有限公司通过砺思资本管理的天津砺思星深基金认缴 5 亿元参与；上述融资信息尚未获得 DeepSeek 官方确认。

telegram · zaihuapd · 11月27日 06:33

**「背景」** 据《The Information》报道，DeepSeek 在今年 6 月完成了约 510 亿元人民币的首轮融资（来源 tool-1-1）；据观察者网引用企查查信息，本轮 1055 亿元的募资规模再次刷新中国 AI 行业单轮融资纪录（来源 tool-1-3）。

**「影响」** 若交易完成，蜜雪冰城将以 5 亿元认缴额通过天津砺思星深基金间接持有 DeepSeek 少数权益，这使其部分资金与 DeepSeek 约 6155 亿元投后估值的波动挂钩，而与其茶饮门店经营无直接关系。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.ithome.com/1/020/121.htm">曝 DeepSeek 第 二 轮 融 资 1055 亿 元 ： 估 值 6155 ...</a></li>
<li><a href="https://www.guancha.cn/CaiJing/2026_11_19_909123.shtml">31名股东排队参 投 ， DeepSeek 最新 估 值 超6000 亿</a></li>
<li><a href="https://news.mbalib.com/story/258976">早报|苹果 AI 入华牵手阿里千问; DeepSeek 估 值 6155 ...</a></li>

</ul>
</details>

**标签**: `#DeepSeek`, `#Mixue`, `#venture financing`, `#AI`, `#valuation`

---

<a id="item-finance-news-3"></a>
### [央行发布大额存单新规 个人起购门槛降至 10 万元](https://www.news.cn/fortune/20261127/70789d77822242cc82216f51a416f872/c.html) ⭐️ 7.0/10

中国人民银行 11 月 27 日公布《大额存单管理办法》，将个人投资人认购起点定为不低于 10 万元、机构不低于 500 万元，两个门槛均较原规定下调一半，自 2027 年 3 月 21 日起施行。

telegram · zaihuapd · 11月27日 11:36

**「背景」** 现行 2015 年暂行办法规定的个人、机构认购起点分别为 20 万元和 1000 万元；同日发布的《人民币存贷款利率管理规定》要求金融机构自主定价、不得高息揽储，并与新办法同日施行。

**「影响」** 对银行而言，禁止高息揽储将限制其通过抬高存款利率争夺存款的空间；对个人储户而言，10 万元起购使部分此前达不到 20 万元门槛的储户可参与大额存单。

**标签**: `#大额存单`, `#中国人民银行`, `#存款利率`, `#银行监管`, `#个人储蓄`

---