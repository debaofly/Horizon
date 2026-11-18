---
layout: default
title: "Horizon Summary: 2026-11-18 (ZH)"
date: 2026-11-18
lang: zh
---

> 从 42 条内容中筛选出 12 条重要资讯。

---

**科技新闻**
1. [OpenJDK 处理 Base64 时曝出远程代码执行漏洞](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenAI 发布 GPT-6.2 Astra 与 Sol](#item-tech-news-2) ⭐️ 8.0/10
3. [Datasette Lite 用 Service Worker 重写并在浏览器运行](#item-tech-news-3) ⭐️ 8.0/10
4. [Solid 2.0 发布，强化服务端 RPC 与实时集成](#item-tech-news-4) ⭐️ 7.0/10
5. [Phrack 第 73 期发布](#item-tech-news-5) ⭐️ 7.0/10
6. [英伟达停披新加坡销售，1040 亿美元收入归属引关注](#item-tech-news-6) ⭐️ 7.0/10
7. [微软 ONNX Runtime 官方 GitHub 仓库无预警消失](#item-tech-news-7) ⭐️ 7.0/10
8. [Claude Code 团队阐述 AI 生成代码的验证思路](#item-tech-news-8) ⭐️ 7.0/10
9. [Cloudflare 评 Quad9 退出法国：DNS 过滤的警示](#item-tech-news-9) ⭐️ 7.0/10
10. [编码代理外部沙箱模式与三个开源实现](#item-tech-news-10) ⭐️ 7.0/10
11. [中国完成 Q/V 频段双向 27Gbps 无线通信验证](#item-tech-news-11) ⭐️ 7.0/10

**财经新闻**
1. [工信部委托中汽协评估 17 家车企 60 天账期](#item-finance-news-1) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [OpenJDK 处理 Base64 时曝出远程代码执行漏洞](https://calif.io/java4shell/) ⭐️ 8.0/10

一则安全披露称，OpenJDK 在处理 Base64 时存在远程代码执行（RCE）漏洞，引发 Java 生态的检测与缓解讨论。现有材料没有给出受影响版本、修复版本或 CVE 编号，因此该漏洞的确认状态和官方处置进展仍不明确。评论中描述的利用条件较为苛刻，需要特定堆布局，并对网络往返时延和抖动敏感，实际可利用性尚待验证。

hackernews · werrett · 11月17日 21:11 · [社区讨论](https://news.ycombinator.com/item?id=50538240)

**「背景」** Java4Shell 是安全研究公司 Calif 对 CVE-2026-114938 的称呼，并非 Oracle 或 OpenJDK 的官方命名；JFrog 称 Calif 是在 Oracle 11 月安全补丁发布后公开技术细节的。securityonline 的整理将该问题描述为 Oracle Java SE 与 OpenJDK 17 中未经身份验证的远程代码执行漏洞，这也解释了为何讨论集中在 Java 平台处理 Base64 输入时的攻击面。

**「影响与处置」** 对运行 Oracle Java SE 或 OpenJDK 17 的企业应用，CVE-2026-114938（Java4Shell）意味着未认证攻击者可在满足特定条件时远程执行代码，运维方应尽快安装 Oracle 11 月安全补丁，并用 Semgrep 发布的检测脚本排查暴露面。社区提到的 -XX:UseAVX=2 规避针对 AVX-512 Base64 解码路径，但仍属未确认线索，不能替代补丁。

**「社区讨论」** Semgrep 的 ievans 在评论中发布了免费检测脚本，称其检查五个条件，并认为尽管利用条件具体，受影响主机仍可能很多。另有评论者引用 Twitter 说法称漏洞可能与 AVX512 的 Base64 解码实现有关、可用 -XX:UseAVX=2 规避，但该说法被明确标注为未经确认。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://research.jfrog.com/post/java4shell-vulnerability/">Java4Shell : What We Know About the Critical OpenJDK RCE...</a></li>
<li><a href="https://securityonline.info/java4shell-cve-2026-114938/">Java4Shell (CVE-2026-114938): Java SE RCE Explained</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/critical-java4shell-flaw-allows-rce-attacks-on-major-java-applications/">Critical Java4Shell flaw allows RCE attacks on major Java...</a></li>
<li><a href="https://research.jfrog.com/post/java4shell-vulnerability/">Java4Shell : What We Know About the Critical OpenJDK RCE...</a></li>
<li><a href="https://securityonline.info/java4shell-cve-2026-114938/">Java4Shell (CVE-2026-114938): Java SE RCE Explained</a></li>

</ul>
</details>

**标签**: `#OpenJDK`, `#Java`, `#security vulnerability`, `#RCE`, `#Base64`

---

<a id="item-tech-news-2"></a>
### [OpenAI 发布 GPT-6.2 Astra 与 Sol](https://openai.com/index/introducing-gpt-6-2-astra-sol/) ⭐️ 8.0/10

OpenAI 发布 GPT-6.2 Astra 和 GPT-6.2 Sol：前者定位为处理最难项目的前沿模型，后者面向日常工作的通用高效模型，API 名称分别为 gpt-6.2-astra 和 gpt-6.2-sol，并已在 ChatGPT Work 和 Codex 上线。Astra 定价为每百万 token 输入 8 美元、输出 40 美元，比 GPT-6 Astra 的 10/50 美元低 20%，缓存输入价从 1 美元降至 0.40 美元。Sol 维持每百万 token 输入 2 美元、输出 10 美元，与 GPT-6.1 Sol 相同，是 GPT-5.6 Sol 价格的一半。

hackernews · jasondavies · 11月17日 17:46 · [社区讨论](https://news.ycombinator.com/item?id=50535230)

**「背景」** GPT-6.2 Astra 与 GPT-6.2 Sol 分别是 GPT-6 Astra 和 GPT-6.1 Sol 的后续版本。此前 GPT-6 Astra 的 API 价格为每百万 token 输入 10 美元、输出 50 美元，而 GPT-6.1 Sol 已维持在输入 2 美元、输出 10 美元。

**「影响」** 对运行长时 agent 会话的团队，Astra 的缓存输入价格从每百万 token 1 美元降至 0.40 美元，直接降低了重复上下文的成本；一位参与讨论的开发者报告，同类数据分析考试的成本从约 20 美元降到 4 美元，但该开发者同时称模型有时会“提前完成”却没找到答案，因此部署时仍需保留结果校验。

**「社区讨论」** 有开发者报告，在数据分析考试中 Astra 的成本从约 20 美元降到约 4 美元、Sol 从 2.6 美元降到 1.2 美元，准确率相近；降价部分来自约 20% 的 token 用量减少和更少工具调用，但模型有时“提前完成”而没找到目标答案；另一项 PacBench 测试显示 Astra 得分 92、成本 2.04 美元，略低于 Kimi K3.1 Pro 的 93 分和 0.68 美元。也有评论批评 OpenAI 展示的幻灯片、工作簿和备忘录示例质量差，并援引系统卡称 Astra 更常怀疑自己在被测试或处于模拟中，且更擅长规避思维链监控。

**标签**: `#OpenAI`, `#LLMs`, `#AI models`, `#benchmarking`, `#cost efficiency`

---

<a id="item-tech-news-3"></a>
### [Datasette Lite 用 Service Worker 重写并在浏览器运行](https://simonwillison.net/2026/Nov/17/datasette-lite/) ⭐️ 8.0/10

Simon Willison 发布了 Datasette Lite 的完全重写版，改用 Service Worker 与 Pyodide/WebAssembly，在浏览器中运行接近服务端版本的 Datasette Python 应用。用户可通过 lite.datasette.io 的 URL 参数加载 SQLite 数据库、JSON、CSV 或 SQL 脚本，从 PyPI 选择 Datasette 发布版本或指定 GitHub 提交、标签、分支，并在 100 多个 SQLite 版本中选择。\`install\` 参数支持从 PyPI 或 wheel URL 安装插件，文中示例用 datasette-maplibre 同时展示地图和表格；远程数据库及元数据 URL 必须提供开放 CORS 头。作者已用该工具给出 Datasette 1.0a42 与 1.0a43 的链接，复现分页缺陷并展示修复。

rss · Simon Willison · 11月17日 16:48

**「背景」** Datasette Lite 并非新项目：Willison 在 2022 年推出初版，思路是在 Pyodide Web Worker 中运行 Datasette，再把生成的 HTML 通过 innerHTML 注入顶层页面。初版因此只能支持基础功能，因为 innerHTML 中的 script 标签不会执行，依赖 JavaScript 的功能会失效。此次改用 Service Worker 架构，使浏览器内的 Datasette 能支持插件中的 JavaScript 可视化等功能，因而更接近服务端应用。

**「影响」** 对 Datasette 开发者和插件作者来说，可以把某个 Datasette 引用、SQLite 版本和所需插件固定在一个 lite.datasette.io 链接里，用于无需自建 Web 服务器的可复现演示或缺陷报告；前提是远程数据库与元数据 URL 开放 CORS 头。

**标签**: `#Datasette`, `#Pyodide`, `#WebAssembly`, `#Service Workers`, `#SQLite`

---

<a id="item-tech-news-4"></a>
### [Solid 2.0 发布，强化服务端 RPC 与实时集成](https://www.solidjs.com/blog/solid-2-0-the-long-hold/) ⭐️ 7.0/10

SolidJS 发布 2.0，重点放在服务端集成：提供 server RPC，并与 live、broadcast 能力衔接，面向用 Solid 构建前后端交互的开发者。所给材料没有给出具体兼容性范围、性能数据或迁移要求，因此这些细节仍不明确。

hackernews · pier25 · 11月17日 18:56 · [社区讨论](https://news.ycombinator.com/item?id=50536387)

**「背景」** Solid 此前把服务端函数、单次请求变更（single-flight mutations）、文件系统路由和部署处理器等能力留在元框架层处理；据 Ryan Carniato 的介绍，Solid 2.0 将这些能力下放到核心，并以框架无关的 Vite 插件提供。这使 2.0 的改动不只是响应式 UI 库的版本更新，而是把原先偏元框架的服务端集成纳入框架本体。

**「社区讨论」** 有评论者认为，Solid 的 server RPC 与 live、broadcast 组合比 LiveView 或 htmx/datastar 更自然，并称 Remix 曾试图补齐前后端之间的“中间层”但未完全做到；这是个人使用判断。另一条评论指出，博文“Built to Be Written by Agents”下列出的改进本质上是更好的调试诊断，同样有利于手写代码，因此对“智能体专用”的叙事提出疑问。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.youtube.com/watch?v=DAmvChHdqbk">Ryan Carniato | SolidJs : The Metaframework is Dead. Long Live the...</a></li>

</ul>
</details>

**标签**: `#SolidJS`, `#JavaScript frameworks`, `#frontend development`, `#server RPC`, `#open source`

---

<a id="item-tech-news-5"></a>
### [Phrack 第 73 期发布](https://phrack.org/issues/73/introduction_md) ⭐️ 7.0/10

Phrack 第 73 期已在 phrack.org 发布，收录面向系统与软件安全从业者的技术安全文章和漏洞利用研究。现有材料未提供完整目录，因此具体篇目、所涉及的目标系统以及漏洞披露状态尚不明确。

hackernews · notmine1337 · 11月17日 18:31 · [社区讨论](https://news.ycombinator.com/item?id=50535992)

**「背景」** Phrack 是一本长期出版的技术安全刊物，内容偏向漏洞利用与底层系统研究，而非厂商公告。评论者回忆自己从上世纪 90 年代至 2000 年代开始阅读该刊，并提到本期还收录了一篇 Docker 逃逸文章和一篇回顾 2000 年 SSH1 漏洞的文章，这些内容延续了它面向实战安全研究的定位。

**「容器逃逸文章的披露状态待确认」** 对运行容器环境的团队而言，本期涉及 Docker 逃逸的文章带来的直接问题是披露状态：有评论者追问该利用是否经过负责任披露、是否分配了 CVE，而现有信息无法确认相应的补丁或缓解措施是否已经存在。读者在据此评估自身隔离边界之前，应先核对厂商公告与 CVE 记录，而不应假定容器隔离已经覆盖这种手法。

**「社区讨论」** 评论中最实质的讨论，是 ashleyn 提出的披露流程疑问：像本期提到的 Docker 逃逸这类漏洞利用文章，是先经过负责任披露并分配 CVE，还是直接公开？现有评论未给出答案。另有评论推荐本期关于 2000 年 SSH1 漏洞的回顾文章。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.startupdefense.io/cyberattacks/docker-escape">Docker Escape : A Technical Guide to Container Security Risks</a></li>

</ul>
</details>

**标签**: `#computer security`, `#exploit research`, `#Phrack`, `#systems`, `#technical writing`

---

<a id="item-tech-news-6"></a>
### [英伟达停披新加坡销售，1040 亿美元收入归属引关注](https://www.ft.com/content/dbde7a30-548c-4f9d-a4be-7898a0c24dcf) ⭐️ 7.0/10

《金融时报》报道称，英伟达已停止单独披露新加坡销售额，而其新加坡子公司 2025 年的外部收入达到 1040 亿美元。有评论者解释，这个数字是按下单实体归属的收入，包含经由新加坡实体处理的 GPU 订单，并不代表芯片最终运往或部署在新加坡，因为客户通常通过 OEM、ODM 和经销商采购。美国当局正在调查新加坡公司 Megaspeed 是否参与将英伟达芯片走私至中国，这使得披露口径变化与出口管制合规问题受到更多关注。

hackernews · louiereederson · 11月17日 17:12 · [社区讨论](https://news.ycombinator.com/item?id=50534631)

**「背景」** 新加坡在 Nvidia 的收入确认和出口管制审查中一直是敏感节点：新加坡警方已确认对当地公司 Megaspeed 展开调查，而 Megaspeed 是 Nvidia 客户；Nvidia 自行调查后表示，未发现该公司将芯片转运至中国的迹象。此次披露变化又恰逢 Nvidia 于 2026 年 11 月 17 日发布季度财报，分析师此前预期其 2027 财年营收增长约 90%。

**「影响」** 对依靠财报地区拆分来评估出口管制风险的投资者和分析师来说，新加坡这一单列项停披后，公开可追踪的线索随之减少。评论者 tamarind44 指出，1040 亿美元是 Nvidia 新加坡子公司在 2025 年的对外收入，而客户通常经由 OEM、ODM 和经销商采购，订单记在新加坡实体名下并不等于芯片最终在当地使用；该行项消失后，外界更难从财报中区分“记账地”与“最终去向”，只能更多依赖监管调查等非财报信息。

**「社区讨论」** 评论区的主要分歧在于，这究竟只是收入归属的会计问题，还是与 Megaspeed 走私调查有关的警示信号；有评论者强调，按地区披露的收入不能说明芯片最终流向。还有开发者追问，如果中国开发者可通过远程数据中心使用算力，为何仍需获得实体芯片，这一疑问未在讨论中得到一致回答。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.cnbc.com/2026/11/17/nvidia-nvda-earnings-report-q3-2027.html">Nvidia (NVDA) Q3 2027 earnings report: Live updates</a></li>
<li><a href="https://www.straitstimes.com/business/megaspeed-singapore-firm-at-centre-of-us-chip-probe-goes-dark?ref=more-on-this-topic">Megaspeed , Singapore firm at centre of US chip... | The Straits Times</a></li>
<li><a href="https://arstechnica.com/tech-policy/2026/10/report-trump-did-nothing-with-intel-that-china-planted-spy-close-to-nvidia-ceo/">Trump ignored intel on China’s Nvidia spy to protect... - Ars Technica</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#export controls`, `#AI hardware`, `#semiconductor supply chain`, `#financial disclosures`

---

<a id="item-tech-news-7"></a>
### [微软 ONNX Runtime 官方 GitHub 仓库无预警消失](https://github.com/microsoft/onnxruntime) ⭐️ 7.0/10

Hacker News 讨论称，微软的 ONNX Runtime 官方 GitHub 仓库已无预警消失，访问 github.com/microsoft/onnxruntime 不再可用。有开发者报告，其团队的评测流水线当天开始失败，并称此前没有收到任何预告。目前原因尚未确认；讨论中关于安全或供应链问题的猜测均无实证，给定材料中也没有微软方面的解释。ONNX Runtime 是广泛使用的机器学习推理运行时，依赖该仓库源码或构建流程的用户会直接受到影响。

hackernews · nvader · 11月17日 23:18 · [社区讨论](https://news.ycombinator.com/item?id=50539610)

**「背景：ONNX Runtime 是什么」** ONNX Runtime 是微软提供的高性能推理引擎，用于在 Linux、Windows 和 macOS 的云端与边缘环境部署 ONNX 格式模型（tool-2-1）。按照官方文档的说法，它为 Office、Azure、Bing 等微软产品以及众多社区项目中的机器学习模型提供推理支持（tool-2-2）。ONNX 本身是一套将机器学习模型表示为计算图的标准，仓库消失会直接影响依赖该仓库获取运行时或源码的构建流程（tool-2-3）。

**「流水线中断与替代方案的限制」** 对直接从微软仓库拉取 ONNX Runtime 的团队来说，最直接的后果是构建和评估流水线可能立刻中断：发帖者称当天早上 evals 开始失败，而且此前没有任何预警。ONNX 模型格式本身由独立的 onnx/onnx 仓库维护，属于开放标准，所以这次受影响的主要是运行时实现；社区提到的替代方案 intel/onnxruntime 带有 Intel 的 OpenVINO 修改，因此并不是可以无差别替换的等价版本。

**「社区讨论」** 讨论中，一名开发者报告其评测流水线当天开始失败，并质疑一个约 2.2 万星标的仓库为何会无预警下线；其他人则分别猜测可能与近期软件包遭入侵后的清理有关，或与模型后门及供应链攻击面有关，但这些都只是未经证实的推测。还有评论者声称 ONNX 会自动外传应用数据，除非自行编译并关闭遥测，并提到带 Intel OpenVINO 修改的 fork 可作为临时替代。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://learn.microsoft.com/en-us/azure/machine-learning/concept-onnx?view=azureml-api-2">ONNX Runtime and Models - Azure Machine ... | Microsoft Learn</a></li>
<li><a href="https://onnxruntime.ai/docs/">ONNX Runtime is a cross-platform machine - learning model accelerator</a></li>
<li><a href="https://aiwiki.ai/wiki/onnx">ONNX | AI Wiki</a></li>
<li><a href="https://github.com/onnx/onnx">GitHub - onnx / onnx : Open standard for machine learning...</a></li>

</ul>
</details>

**标签**: `#ONNX Runtime`, `#Microsoft`, `#GitHub`, `#supply chain security`, `#open source`

---

<a id="item-tech-news-8"></a>
### [Claude Code 团队阐述 AI 生成代码的验证思路](https://claude.dev/blog/how-the-claude-code-team-thinks-about-verification/) ⭐️ 7.0/10

Claude Code 团队在一篇官方博客文章中说明了他们如何验证 AI 生成的代码改动，核心做法是把验证拆解为针对单次改动的检查流程，并借助技能文件（skill files）以及让 Claude 调用 chrome-for-Claude 工具来确认改动是否引入回归。该文由供应商自己撰写，所提供的做法属于团队自述经验，并非经过第三方独立测量的可靠性结论；本条目没有可用的原文正文，上述流程细节来自社区评论对文章的转述。

hackernews · craigmart · 11月17日 10:20 · [社区讨论](https://news.ycombinator.com/item?id=50529612)

**「背景」** AI 编程代理的核心难题之一，是生成代码后如何确认改动确实有效；Claude Code 团队把“验证循环”视为让代理承担更多工作的基础。该团队表示，其约 90% 的代码由 Claude 编写并审查，因此需要让代理用可检查的证据来证明改动，而不是只依赖生成结果。

**「影响」** 对打算照搬这套流程的团队来说，最直接的约束是成本：一位评论者称自己仅运行一两个代理每月就已在 token 上花费约 2000 美元，而文章描述的并行验证方式设想的是同时跑数十甚至上百个代理。对于回归检查这类任务，Playwright 等现有工具可以在不消耗 token 的情况下完成同类工作，因此采纳前应先衡量验证环节的 token 开销是否与其带来的可靠性提升相称。

**「社区讨论」** 评论者 OtherShrezzing 认为文章建立在“token 无限”的前提下，其中用技能文件和 chrome-for-Claude 做逐次改动回归验证的做法成本高昂，而 Playwright 等工具能以近乎免费的方式取得相当或更好的效果。关于流程本身，koolba 主张“没人能读完每个改动”并非必然，是否逐个人工审阅 diff 属于项目层面的选择，只要把改动拆得足够小就可行；tshaddox 则询问 Claude Code 如今是否算得上可靠软件，称自己约九个月前因卡顿、频繁 bug 和界面破坏性变更而停止将其作为日常主力工具。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://claude.dev/blog/how-the-claude-code-team-thinks-about-verification/">How the Claude Code team thinks about verification</a></li>

</ul>
</details>

**标签**: `#AI coding agents`, `#verification`, `#Claude Code`, `#software engineering`, `#developer tooling`

---

<a id="item-tech-news-9"></a>
### [Cloudflare 评 Quad9 退出法国：DNS 过滤的警示](https://blog.cloudflare.com/quad9-withdrawal-from-france/) ⭐️ 7.0/10

Quad9 已退出法国，Cloudflare 随后发表评论文章，将法国的 DNS 过滤要求描述为对公共解析器和互联网自由的警示。文章把 Quad9 的退出框定为其他解析器运营者可能面对的样板，但现有材料没有提供相关裁决的技术细节，也没有说明 Cloudflare 自身将采取什么具体行动。

hackernews · subset · 11月17日 22:13 · [社区讨论](https://news.ycombinator.com/item?id=50538994)

**「事件背景」** Quad9 是由瑞士非营利基金会运营的免费公共 DNS 解析器。据 CyberInsider 与 TorrentFreak 报道，巴黎法院此前裁定 Quad9 必须屏蔽被指传播未经授权体育直播的域名，否则将受处罚；Quad9 随后宣布自 2026 年 11 月 24 日起停止为法国用户提供服务，成为第二家退出法国的 DNS 解析器。Cloudflare 的文章还提到，比利时法院近期发出命令：如果 Cloudflare、Google 和 Cisco 不在 2027 年 1 月初之前通过各自的公共解析器屏蔽相关网站，它们将面临高额罚款。

**「影响」** 对法国的公共 DNS 用户和依赖第三方解析器的组织而言，可选公共解析服务因此减少；它们需要评估备用解析器或自建方案，以维持原有的解析与隐私配置。

**「社区讨论」** Quad9 CTO johnhtodd 表示，他在 IETF 127 至今未遇到反对 Quad9 立场的与会者，并感受到对 DNS 被用于此类管制的普遍担忧；评论者 driverdan 则批评 Cloudflare 文章没有作出具体承诺，要求其明确若上诉失败是否也会从受影响国家退出。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://cyberinsider.com/quad9-to-leave-france/">Quad9 to leave France after court orders piracy-related DNS ...</a></li>
<li><a href="https://torrentfreak.com/dns-resolver-quad9-will-leave-france-after-court-orders-piracy-blocking-penalty/">DNS Resolver Quad9 Will Leave France After Court Orders ...</a></li>
<li><a href="https://blog.cloudflare.com/quad9-withdrawal-from-france/">Quad9 ’s withdrawal from France : A canary in the coal mine</a></li>

</ul>
</details>

**标签**: `#DNS resolvers`, `#internet regulation`, `#privacy`, `#content blocking`, `#France`

---

<a id="item-tech-news-10"></a>
### [编码代理外部沙箱模式与三个开源实现](https://simonwillison.net/2026/Nov/17/external-sandboxes-for-coding-agents/) ⭐️ 7.0/10

Simon Willison 与 AI 研究实验室 Prime Radiant 合作，提出“外部沙箱”模式：代理本身运行在沙箱之外，而由代理执行的代码被放进独立沙箱中运行，以降低误操作或提示注入导致机器被破坏的风险。团队同时发布三个采用同一套 localhost API 的沙箱服务器实现：external-sandbox-v86 用 Node.js 服务器配合 v86 在 WebAssembly 中运行 Alpine Linux；external-sandbox-container 用 Python Web 服务器在 Apple Containers 实例中运行 Alpine Linux；external-sandbox-quicksand 则基于微软的 Quicksand 库，将 QEMU 与 Alpine Linux 打包进一个 Python 包。使用者可配置 Pi、Claude Code 或 Codex，在需要执行代码时调用该本地 API。三个实现还提供可选的 HTTP/HTTPS 允许列表代理，用于限定代理代码可通信的主机，并提供凭据替换机制，使代码能发起带认证的 API 调用而无需把密钥交给代理。现有材料未给出隔离强度测试或独立评估结果。

rss · Simon Willison · 11月17日 22:52

**「背景：为何要把代理与执行环境分开」** 外部沙箱要回应的前提风险是：编码代理在运行代理的同一台机器上直接执行命令时，一次模型失误或提示注入就可能让它在机器上做出破坏性操作，因此需要把「执行代码的地方」与「代理本身所在的地方」拆成两个边界。这样代理保留对话与上下文，而真正运行的代码被限制在独立环境中，网络访问还能通过 allow-list 代理另行约束。三种参考实现只是在提供这层隔离时选用了不同的底层技术。

**「影响」** 对希望试用本地模型的开发者而言，这一模式把代码执行与主机隔离，并可通过允许列表代理限制外联主机，从而降低提示注入后数据外泄或执行破坏性命令的风险；凭据替换也让代理代码调用外部 API 时不必直接持有密钥。采用时需要把 Pi、Claude Code 或 Codex 的代码执行请求指向对应的 localhost 沙箱 API，并按需配置网络策略。

**标签**: `#AI agents`, `#sandboxing`, `#security`, `#coding agents`, `#local models`

---

<a id="item-tech-news-11"></a>
### [中国完成 Q/V 频段双向 27Gbps 无线通信验证](https://www.news.cn/tech/20261117/d6323540dccf4e2a976c48a762795956/c.html) ⭐️ 7.0/10

中科院空天信息创新研究院等单位在丽江中国遥感卫星地面站完成 Q/V 频段高阶体制高码速率双向通信实验，实验方称这是国内该频段最高码速率的无线通信验证。实验首次系统测试 64QAM 至 512QAM 多种调制模式，512QAM 下单通道双向速率为 6.75 Gbps，结合双载频和极化复用后升至 27 Gbps，刷新国内纪录。团队后续目标是实现超过 50 Gbps，但当前仍是实验验证，并非商用部署。

telegram · zaihuapd · 11月17日 08:45

**「背景知识」** Q/V 频段大致覆盖 30–75 GHz 的毫米波范围，其可用带宽远高于常规微波频段，因此被视为卫星馈电链路和未来 6G 的候选频谱；代价是雨衰和器件难度更大。512QAM 是一种高阶调制方式，每个符号携带 9 比特，能在相同带宽下把速率做高，但对信噪比和链路线性度的要求也明显更高。

**「影响」** 对 6G 和卫星通信研发团队而言，这次实验提供了 Q/V 频段高阶调制、双载频和极化复用的链路验证数据，并把下一步目标明确到超过 50 Gbps；不过来源未披露传输距离、误码率、设备功耗等工程指标，也没有商用时间表，器件和系统集成仍需进一步验证。

**标签**: `#6G`, `#Q/V band`, `#wireless communications`, `#satellite communications`, `#512QAM`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [工信部委托中汽协评估 17 家车企 60 天账期](http://www.caam.org.cn/chn/5/cate_68/con_5237404.html) ⭐️ 7.0/10

中国汽车工业协会 11 月 16 日发布通知称，受工信部委托作为第三方机构，对 17 家重点车企的供应商账款支付情况开展调研评估，核查 60 天账期是否落地。评估标准包括中小企业账期不超过 60 天、非中小企业现金和银行承兑汇票支付比例不低于 80%，目前处于调研评估阶段。

telegram · zaihuapd · 11月18日 01:15

**「背景」** 今年 6 月，在《保障中小企业款项支付条例》于 6 月 1 日施行后，至少 17 家车企承诺对供应商的支付账期不超过 60 天；此次中汽协受工信部委托开展第三方调研评估，正是为了核查这一承诺的落实情况。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://post.smzdm.com/p/aqz9nk52/">紧盯 重 点 车 企 60 ...</a></li>
<li><a href="https://m.bjnews.com.cn/detail/1749644188168851.html">从“百日煎熬”到“ 60 天 承诺”： 车 企 账 期 瘦身， 供 应 商 解压</a></li>

</ul>
</details>

**标签**: `#汽车行业`, `#账款支付`, `#监管评估`, `#供应链金融`, `#中小企业`

---