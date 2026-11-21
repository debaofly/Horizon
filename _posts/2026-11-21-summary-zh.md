---
layout: default
title: "Horizon Summary: 2026-11-21 (ZH)"
date: 2026-11-21
lang: zh
---

> 从 39 条内容中筛选出 14 条重要资讯。

---

**科技新闻**
1. [Inkling 2 Mini：开放权重的循环 Transformer 小模型](#item-tech-news-1) ⭐️ 8.0/10
2. [Anthropic 的 Alpöge 声称借助 Claude 证明广义黎曼猜想](#item-tech-news-2) ⭐️ 8.0/10
3. [GitHub 仓库声称纳维–斯托克斯方程有限时间爆破，尚待验证](#item-tech-news-3) ⭐️ 8.0/10
4. [KVM 漏洞 CVE-2026-99312：AMD 嵌套虚拟化主机内存可被虚拟机读取](#item-tech-news-4) ⭐️ 8.0/10
5. [台积电暂停中国客户 16nm 及以下芯片订单](#item-tech-news-5) ⭐️ 8.0/10
6. [美国 SEC 据报审查英伟达潜在会计问题](#item-tech-news-6) ⭐️ 7.0/10
7. [Signal 推动限制 AI 代理抓取移动端聊天数据](#item-tech-news-7) ⭐️ 7.0/10
8. [Tao 讨论无外力 Navier–Stokes 奇点与广义黎曼猜想](#item-tech-news-8) ⭐️ 7.0/10
9. [美国收紧芯片出口，印度 Yotta 拟一年增 10 万块 GPU](#item-tech-news-9) ⭐️ 7.0/10
10. [苹果被曝研发主动式 AI 智能体，最早 2027 年末推出](#item-tech-news-10) ⭐️ 7.0/10

**科技博客**
1. [输出缓存为何难以奏效](#item-tech-blog-1) ⭐️ 6.0/10

**财经新闻**
1. [沃什避免前瞻指引，美联储官员却更频繁公开谈论加息](#item-finance-news-1) ⭐️ 7.0/10
2. [美国企业转向净发行股票，新增供给或成牛市逆风](#item-finance-news-2) ⭐️ 7.0/10
3. [北京拟规定租房正常损耗不得扣减押金](#item-finance-news-3) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Inkling 2 Mini：开放权重的循环 Transformer 小模型](https://thinkingmachines.ai/news/inkling-2-mini/) ⭐️ 8.0/10

开放权重的小模型 Inkling 2 Mini 已发布，据报道采用循环 Transformer 架构，目标之一是改善本地部署体验。社区用户称在 Ryzen 395 上通过 llama.cpp 的 Vulkan 后端达到约 27 tokens/s 解码速度，并在 32GB M1 Pro 上以 q4 量化获得约 10 tokens/s。所谓“达到 Qwen3.8-27B 水平”的基准说法和上述吞吐均来自初步用户测试或转述，尚缺独立验证，模型参数、许可证和官方基准细节在现有材料中也不完整。

hackernews · jasondavies · 11月20日 20:12 · [社区讨论](https://news.ycombinator.com/item?id=50581260)

**「背景：循环 Transformer 与 Inkling 系列」** 循环 Transformer 的核心做法是让模型的中间层重复执行多次，使每个 token 上都进行更多计算，从而用更少的 token 得出答案；这是理解 Inkling 2 Mini 架构选择的前提。Inkling 2 Mini 属于 Thinking Machines 的 Inkling 开放权重模型系列，该系列此前已在 Tinker 平台上提供文本、图像和音频模型的微调。

**「本地部署仍需自行打补丁」** 想在本地运行 Inkling 2 Mini 的用户目前要自己编译带未合并 PR（32694、32657、32429、32704）的 llama.cpp，并额外打上社区补丁才能在 Vulkan 后端获得约 30% 的提速；实测解码速度在 Ryzen 395 上约为 27 tokens/s，在 32GB M1 Pro 上约为 10 tokens/s，因此硬件和后端选择会直接决定它是否可用。由于循环式（looped）结构会多次复用同一组 transformer 层，实际每 token 的计算量取决于循环次数，而不只取决于参数量，这也意味着这类模型的性能调优更多落在推理框架与补丁上。unsloth 发布的 GGUF 量化版本已可在 Ollama/llama.cpp 上运行。

**「社区讨论」** 社区讨论主要围绕实际本地表现：hedgehog 报告 Ryzen 395 + llama.cpp Vulkan 约 27 tokens/s，并列出未合并 PR 和一个约 30% 提速的补丁；dgacmu 在 32GB M1 Pro 上约 10 tokens/s，简单 Python 任务成功，但硬币识别测试在约 1.2 万 tokens 后失败。对“达到 Qwen3.8-27B 水平”的说法，montroser 明确以“如果基准在真实场景中成立”为前提，其他评论也尚未形成一致结论。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://thinkingmachines.ai/news/inkling-2-mini/">Introducing Inkling 2 Mini - Thinking Machines Lab</a></li>
<li><a href="https://thinkingmachines.ai/inkling/">Inkling - Thinking Machines Lab</a></li>
<li><a href="https://sebastianraschka.com/llm-architecture-gallery/looped-depth-sharing/">Looped Transformer | Sebastian Raschka, PhD</a></li>

</ul>
</details>

**标签**: `#open-weight models`, `#looped transformers`, `#local inference`, `#llama.cpp`, `#model efficiency`

---

<a id="item-tech-news-2"></a>
### [Anthropic 的 Alpöge 声称借助 Claude 证明广义黎曼猜想](https://alpo.ge/remark.pdf) ⭐️ 8.0/10

2026 年 11 月 20 日，Anthropic 数学家 Levent Alpöge 发布文稿，声称在与 Claude 合作下证明了黎曼猜想，并将该方法扩展至广义黎曼猜想。他称相关论证已在 Lean 中无假设完成形式化，证明文稿超过 25 万页；社区评论给出的 Lean 归档约为 1.3GB、1500 万行。上述内容目前仍是作者的单方面声明，尚未经过独立验证，不能视为已确立的数学结果。

hackernews · iamronaldo · 11月20日 14:16 · [社区讨论](https://news.ycombinator.com/item?id=50574968)

**「背景」** 黎曼猜想由黎曼于 1859 年提出，断言黎曼 ζ 函数的非平凡零点都落在临界线 Re\(s\)=1/2 上，这直接约束素数的分布；广义黎曼猜想把这一断言推广到更广的一类 L 函数。Lean 是交互式定理证明器，可把证明写成机器可逐步检查的形式，但形式化检查通过仍取决于形式陈述是否忠实对应原猜想以及所依赖的公理。

**「验证状态」** 对形式验证社区而言，当前可操作的步骤是审计 Lean 定理陈述，而非直接采信结论：MIT 的 Andrew Sutherland 已在验证页报告，公开的 Lean 源码可无错误编译，但截至 2026-11-20 19:45 UTC 其余检查仍在进行，页面将随检查完成而更新。能通过 Lean 内核检查只说明证明项与其所写陈述相符，尚不能确认这些陈述确实对应黎曼猜想与广义黎曼猜想。

**「社区讨论」** 评论中最具体的贡献是给出了 Lean 证明归档的规模，并有人链接到一项据称完全由人类完成的替代证明；另有评论引用陶哲轩此前的表态，即 AI 短期内难以攻克黎曼猜想，与这次声称形成对照。对验证状态则有分歧：一名评论者援引 MIT 的 Andrew Sutherland 的检查页面，认为多种形式验证已足以消除疑问，但这仍是社区判断，不等同于独立确认。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.scientificamerican.com/article/anthropic-mathematician-claims-to-prove-riemann-hypothesis-most-famous-problem-in-all-of-math/">Anthropic mathematician claims to prove Riemann hypothesis , most...</a></li>
<li><a href="https://math.mit.edu/~drew/grh/">RH Lean proof: verification files - MIT Mathematics</a></li>

</ul>
</details>

**标签**: `#formal verification`, `#Lean theorem prover`, `#Riemann Hypothesis`, `#mathematics`, `#unverified claim`

---

<a id="item-tech-news-3"></a>
### [GitHub 仓库声称纳维–斯托克斯方程有限时间爆破，尚待验证](https://github.com/tristanbuckmaster/navier-stokes/) ⭐️ 8.0/10

Hacker News 上出现一条链接，指向 GitHub 仓库「Finite-time blow-up for the Navier–Stokes equations」（路径作者名为 tristanbuckmaster），标题声称给出了纳维–斯托克斯方程的有限时间爆破结果。但所给材料只有仓库链接和论坛讨论串，既没有论文、证明细节，也没有独立验证或同行评审信息，因此这是一项尚未证实的主张，而非已确立的数学结果。讨论中提到的其他同日成果同样只来自评论者转述。

hackernews · trotro · 11月20日 15:34 · [社区讨论](https://news.ycombinator.com/item?id=50576232)

**「背景」** 纳维–斯托克斯存在性与光滑性问题是千禧年数学难题之一：它问三维空间中从光滑初值出发的解是否可能始终光滑，而有限时间爆破正是对该问题给出否定答案。2026 年 9 月，OpenAI 公布了一个由内部系统生成、并附有 Lean 形式化的有限时间奇点结果；10 月《科学美国人》援引数学家的报道则认为该结果与 Córdoba–Martínez-Zoroa 的路线不同。此次仓库声称针对无外力情形，并同时提供论文和 Lean 4 形式化，但这些材料是否成立仍需同行评审和独立验证。

**「社区讨论」** 评论者 tancop 称该仓库针对的是「无外力」版本的问题，并把 OpenAI 此前的结果描述为借助精心设计的外力使方程失效；这一对比在材料中未获证实，属于评论者说法。xianshou 与 jrflo 则把当天流传的多项声明（包括广义黎曼猜想和所谓 Anthropic 千禧年问题传闻）并列比较，对优先权与「抢先」争议表示惋惜，这些同样是未经证实的传闻与个人观点。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://aixiv.online/abs/2611.02204">[2611.02204] Finite-time blow-up for the Navier–Stokes ...</a></li>
<li><a href="https://hotrepo.ai/tristanbuckmaster/navier-stokes">tristanbuckmaster/navier-stokes: Lean 4 formalization of a ...</a></li>
<li><a href="https://en.wikipedia.org/wiki/Navier%E2%80%93Stokes_priority_controversy">Navier–Stokes priority controversy - Wikipedia</a></li>
<li><a href="https://openai.com/index/navier-stokes-solution/">On the Navier–Stokes Millennium Prize Problem | OpenAI</a></li>

</ul>
</details>

**标签**: `#Navier–Stokes equations`, `#mathematics`, `#fluid dynamics`, `#research claim`, `#Hacker News`

---

<a id="item-tech-news-4"></a>
### [KVM 漏洞 CVE-2026-99312：AMD 嵌套虚拟化主机内存可被虚拟机读取](https://thehackernews.com/2026/11/new-linux-kvm-flaw-cve-2026-99312-lets.html) ⭐️ 8.0/10

Linux 内核 KVM 曝出 CVE-2026-99312 漏洞，仅影响启用了嵌套虚拟化的 AMD 主机；研究人员在 DigitalOcean 上从虚拟机内读取到约 127 GB 宿主内存。上游修复已于 11 月 18 日随稳定内核 7.3.5 等版本发布，但 Debian、Ubuntu 等发行版内核尚未包含该补丁。在发行版补丁到位之前，可以通过关闭嵌套虚拟化来规避该漏洞。

telegram · zaihuapd · 11月20日 14:23

**「背景」** 嵌套虚拟化是指让虚拟机内部再运行虚拟机的机制，因此 CVE-2026-99312 的影响范围限定在启用该功能的 AMD KVM 主机。Red Hat 指出，KVM 在客户机分页关闭时模拟 INIT 处理器复位仍会重置 MMU 上下文，可能留下仍引用上层虚拟机结构的陈旧状态，使嵌套客户机具备越界访问内存的条件；Red Hat 也因利用条件受限将其评为 Moderate。

**「影响与处置」** 对于启用了嵌套虚拟化的 AMD 主机，升级到包含上游修复的内核是直接处置方式；在 Debian、Ubuntu 等发行版内核尚未跟进时，管理员应关闭嵌套虚拟化作为缓解。这样做会使依赖多级虚拟化的测试和云工作负载暂时不可用，但能消除虚拟机读取宿主内存的暴露面。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://access.redhat.com/security/cve/cve-2026-99312">CVE-2026-99312 - Red Hat Customer Portal</a></li>
<li><a href="https://app.opencve.io/cve/CVE-2026-99312">CVE-2026-99312 - Vulnerability Details - OpenCVE</a></li>
<li><a href="https://www.digitalocean.com/blog/cve-2026-99312-kvm-patch">Virtualization , Responsible Disclosure, and CVE - 2026 - 99312</a></li>

</ul>
</details>

**标签**: `#KVM`, `#Linux kernel`, `#CVE`, `#virtualization security`, `#AMD`

---

<a id="item-tech-news-5"></a>
### [台积电暂停中国客户 16nm 及以下芯片订单](https://appleinsider.com/articles/26/11/20/apple-supplier-tsmc-cuts-off-china-chip-orders-amid-tighter-export-controls) ⭐️ 8.0/10

据该报道，台积电已通知客户暂停接受中国公司的 16nm 及以下先进制程订单；在收紧后的美国半导体出口新规下，除非事先取得美国出口许可或豁免，否则台积电不得供货。此前台积电可自行评估客户设计是否符合豁免条件，现在须由客户提前申请；美国获批名单中虽有苹果、AMD 和英伟达，尚无中国公司。报道称，中国企业因此只能使用 28nm、40nm 等较旧制程，也无法获得 AI 数据中心所需的高带宽内存；台积电表示将遵守新规，但上述消息尚缺独立验证。

telegram · zaihuapd · 11月21日 02:01

**「背景」** 按收紧后的美国半导体出口新规，16nm 及以下先进制程被纳入许可要求；与过去台积电可自行评估客户设计是否满足豁免条件不同，现在客户须提前申请美国许可，已获批名单包括苹果、AMD、英伟达，尚无中国公司。TrendForce 援引《金融时报》称，三星也据称暂停了部分对华消费芯片出货，显示限制可能从 AI 处理器延伸到消费电子。

**「影响」** 中国企业若要在 16nm 及以下节点投片，需自行事先取得美国出口许可或豁免，不能再由台积电逐案评估其设计是否合规，可用的先进制程因此收缩到 28nm、40nm 等成熟节点，AI 数据中心所需的高带宽内存供应也一并受限。TrendForce 的报道指出，此次暂停的影响可能不止于 AI 芯片，还会波及中国客户的消费电子类芯片出货。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://appleinsider.com/articles/26/11/20/apple-supplier-tsmc-cuts-off-china-chip-orders-amid-tighter-export-controls">TSMC has suspended some chip orders amid tighter export controls</a></li>
<li><a href="https://www.trendforce.com/news/2026/11/20/news-tsmc-samsung-reportedly-pause-china-consumer-chip-shipments-under-new-u-s-rules-16nm-orders-affected/">[News] TSMC, Samsung Reportedly Pause China Consumer Chip ...</a></li>
<li><a href="https://www.trendforce.com/news/2026/11/20/news-tsmc-samsung-reportedly-pause-china-consumer-chip-shipments-under-new-u-s-rules-16nm-orders-affected/">[News] TSMC , Samsung Reportedly Pause China Consumer Chip ...</a></li>

</ul>
</details>

**标签**: `#semiconductor export controls`, `#TSMC`, `#China`, `#AI hardware`, `#supply chain`

---

<a id="item-tech-news-6"></a>
### [美国 SEC 据报审查英伟达潜在会计问题](https://www.marketscreener.com/news/us-sec-s-nvidia-probe-is-examining-potential-accounting-issues-sources-say-ce785ed3dd8ff627) ⭐️ 7.0/10

据 MarketScreener 报道，知情人士称美国证券交易委员会（SEC）正在审查英伟达可能存在的会计问题。目前可获得的报道仅有标题层面的信息，调查阶段、具体会计疑点及潜在影响均未得到确认。对投资者和依赖英伟达财务披露的合作伙伴而言，这增加了围绕其财务报告的不确定性，但在监管机构或公司正式确认前不应视为既定事实。

hackernews · ftchd · 11月20日 20:22 · [社区讨论](https://news.ycombinator.com/item?id=50581438)

**「背景」** 据路透社援引两名知情人士的说法，SEC 正在审查英伟达可能存在的会计问题；路透社同时称，这项调查是英伟达近期一系列法律麻烦中的最新一项，美国司法部还在审查其 129 亿美元收购开源平台 Hugging Face 的交易，并对其收购行为展开更广泛的反垄断调查。当前报道把会计审查与围绕英伟达交易和并购行为的另一条监管线索并列，但公开信息尚未说明 SEC 具体质疑哪些会计处理。

**「投资者损失与披露风险」** 对 Nvidia 投资者而言，这则报道已带来可量化的损失：路透报道 SEC 正调查其会计实务后，Nvidia 于 11 月 20 日市值单日蒸发约 5000 亿美元，股价较 10 月的收盘高点下跌约 48%。由于调查仍处于媒体报道阶段、具体细节尚未公开，投资者目前面对的是披露不确定性和后续法律程序风险，而非已确认的会计违规结论。

**「社区讨论」** 评论区中，有人把此事与英伟达此前的循环融资及与 neocloud 的算力交易联系起来，也有评论者质疑让首席财务官出任临时首席执行官是否合适；这些说法均属基于公开传闻的推测，未提供证据。还有人提到以股票换取折扣芯片、大量去向不明的 GPU 等做法，认为问题可能不止会计层面，但同样未经证实。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.investing.com/news/economy-news/exclusiveus-secs-nvidia-probe-is-examining-potential-accounting-issues-sources-say-5042460">Nvidia ’s accounting is a focus of US SEC investigation, sources say...</a></li>
<li><a href="https://www.reuters.com/world/us-secs-nvidia-probe-is-examining-potential-accounting-issues-sources-say-2026-11-20/">Nvidia&#x27;s accounting is a focus of US SEC investigation ...</a></li>
<li><a href="https://www.fool.com/investing/2026/11/20/nvidia-stock-plunge-wipes-out-nearly-usd500-billion-in-one-day-as-sec-reportedly-probes-its-accounting/">Nvidia Stock Plunge Wipes Out Nearly $500 Billion in One Day ...</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#SEC investigation`, `#accounting`, `#tech industry`, `#regulatory risk`

---

<a id="item-tech-news-7"></a>
### [Signal 推动限制 AI 代理抓取移动端聊天数据](https://signal.org/blog/protecting-your-privacy/) ⭐️ 7.0/10

Signal 在一篇隐私博客中表示，正设法限制 AI 代理和移动操作系统平台抓取私人数据，重点是避免第三方 AI 应用读取 Signal 聊天内容。现有材料没有说明具体限制机制、覆盖的 Android/iOS 版本、是否已上线，或 Signal 是否已与操作系统厂商达成合作，因此目前只能确认其公开了该方向，不能确认保护已经生效。对 Signal 用户而言，这一议题涉及同设备上的其他应用或系统级代理能否越过聊天应用边界获取内容。

hackernews · dotcoma · 11月20日 09:42 · [社区讨论](https://news.ycombinator.com/item?id=50572348)

**「背景」** 移动操作系统开始内置 AI agents，Signal 认为这种系统级集成若不受约束，会威胁应用层保护敏感数据的能力（tool-2-1）。Signal 在 11 月 10 日的博客中表示正在限制这些内置 AI agents 获取和存储 Signal 数据（tool-2-3），相关措施包括阻止截图（tool-2-2）。

**「影响」** 影响在于执行层面：如果限制依赖移动操作系统对屏幕读取、无障碍或截图权限的约束，那么同一措施在不同 Android/iOS 版本和厂商定制系统上的效果可能不一致，用户能否得到保护将取决于设备权限设置，而不只取决于 Signal 应用本身。

**「社区讨论」** 评论的争论集中在保护该由谁执行：有用户认为仅靠 Signal 自身限制不够，应让操作系统层收回 AI 应用的访问权，并公开取证结果供其他开发者复用；也有人担心反截图等措施会误伤正常功能，例如 Windows 端无法再截取 Signal 聊天。另有用户报告 Signal 在 VPN 下的验证码问题长期存在，认为这会迫使记者等高风险用户改用其他应用。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://signal.org/blog/protecting-your-privacy/">Signal is Serious About Protecting Your Privacy</a></li>
<li><a href="https://www.inc.com/aaron-mok/signal-blocks-screenshots-ai-agents-privacy/91440348">Signal Blocks Screenshots Over AI Agent Risks - Inc.com</a></li>
<li><a href="https://signal.org/blog/">Signal &gt;&gt; Blog</a></li>

</ul>
</details>

**标签**: `#privacy`, `#mobile security`, `#AI agents`, `#Signal`, `#platform access`

---

<a id="item-tech-news-8"></a>
### [Tao 讨论无外力 Navier–Stokes 奇点与广义黎曼猜想](https://terrytao.wordpress.com/2026/11/20/unforced-euler-singularity-unforced-navier-stokes-singularity-and-the-generalized-riemann-hypothesis/) ⭐️ 7.0/10

Terry Tao 于 11 月 20 日发布博客文章，标题指向无外力 Navier–Stokes 奇点与广义黎曼猜想。由于条目未提供正文，现有材料无法确认文中是否宣布了新证明、给出了哪些成立条件，或只是讨论二者之间的联系。关于证明已被形式化验证的说法目前只见于社区讨论，而非条目正文。

hackernews · archon1410 · 11月20日 17:21 · [社区讨论](https://news.ycombinator.com/item?id=50578358)

**「背景」** Tao 在 2026 年 10 月 4 日的一篇客座博文中已讨论过不可压缩流体的古典解与奇点形成；这篇 11 月 20 日的文章则把“无外力 Euler 奇点”“无外力 Navier-Stokes 奇点”和广义黎曼猜想并列，文章标签还列出 AI、Levent Alpöge、Matei Coiculescu 与 Tristan Buckmaster。由于所给材料没有正文，无法确认新文章的具体定理、证明或验证方式，只能确认它与此前对流体方程奇点问题的讨论直接相关。

**「对 Lean 验证流程的影响」** 对采用 Lean 4 等内核验证 AI 生成证明的团队来说，实际约束是：内核只检查证明项是否合法，不能自动保证形式陈述忠实编码了原本要证的命题；因此工作流中应把“陈述翻译/规格对齐”的人工审查作为独立关卡，否则构建通过并不等于目标结论成立。

**「社区讨论」** 有评论者称，两项独立的内核接受了相关结果，因此认为出现内核漏洞利用的可能性较低；另有评论者追问，面对大规模 Lean 代码，构建通过如何保证形式化的正是目标命题，而不是一个无关的简单陈述。也有科研人员表达了对 AI 进展挤占人类研究空间的焦虑，但这些属于个人判断而非已证实结论。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://terrytao.wordpress.com/2026/11/20/unforced-euler-singularity-unforced-navier-stokes-singularity-and-the-generalized-riemann-hypothesis/">Unforced Euler singularity, unforced Navier-Stokes ...</a></li>
<li><a href="https://terrytao.wordpress.com/2026/10/04/on-classical-solutions-and-singularity-formation-in-incompressible-fluids/">On classical solutions and singularity formation in ...</a></li>
<li><a href="https://mathoverflow.net/questions/513540/should-we-trust-ai-generated-formal-proofs-in-lean-4">Should we trust AI-generated formal proofs in Lean 4?</a></li>
<li><a href="https://mlcrypto.mit.edu/course/scribe-notes/lec14_scribe.pdf">Lecture 14: Lean: A Different Take on Verification</a></li>

</ul>
</details>

**标签**: `#mathematics`, `#Navier-Stokes`, `#Riemann Hypothesis`, `#Lean theorem proving`, `#AI-assisted research`

---

<a id="item-tech-news-9"></a>
### [美国收紧芯片出口，印度 Yotta 拟一年增 10 万块 GPU](https://www.bloomberg.com/news/articles/2026-11-20/nvidia-scandal-fallout-india-ai-yotta-ambani-adani-am-intelligence-e2e-networks) ⭐️ 7.0/10

美国收紧对马来西亚、泰国和新加坡的先进芯片出口之际，印度 AI 业界认为可承接外溢需求。Yotta 表示未来一年将新增约 10 万块 GPU，并称这相当于把印度现有算力提高约 10%。印度目前有 153 个数据中心、居全球第 14，信实承诺投入至多 1100 亿美元、阿达尼 1000 亿美元建设 AI 基础设施，但长期受算力基础设施短缺和资本受限拖累。

telegram · zaihuapd · 11月20日 07:31

**「背景」** 先进 GPU 的跨境采购受美国出口管制约束，而印度本土 AI 算力基础仍较薄弱：目前有 153 个数据中心，居全球第 14，长期受算力基础设施短缺与资本受限拖累。这一供需缺口，是印度业界希望承接外溢需求、并推进大规模 GPU 与数据中心扩张的背景。

**「电力与水资源成关键约束」** 对计划承接外溢需求的印度数据中心运营商而言，新增 GPU 能否按期上线，关键约束在电力与水资源，而非芯片采购本身；数据中心选址、并网和冷却用水安排将直接决定这些算力的实际可用速度。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.ziromarket.com/blog/india-data-center-boom-2026">India Data Center Boom 2026 | Who Benefits | Ziro Market</a></li>
<li><a href="https://government.economictimes.indiatimes.com/news/digital-india/indias-ai-ambitions-need-a-data-centre-boom-but-power-and-water-will-be-the-test/134346376">India &#x27;s Data Centre Boom: Power and Water Challenges for AI ...</a></li>

</ul>
</details>

**标签**: `#AI infrastructure`, `#export controls`, `#India`, `#GPUs`, `#data centers`

---

<a id="item-tech-news-10"></a>
### [苹果被曝研发主动式 AI 智能体，最早 2027 年末推出](https://www.bloomberg.com/news/articles/2026-11-19/apple-is-working-on-ai-agent-for-device-control-apps-browsing-and-coding) ⭐️ 7.0/10

彭博根据苹果本周新增的招聘信息报道，苹果正招募高级工程经理，主导开发一款「主动式 AI 智能体」。该智能体可代用户编写代码、浏览网页并操控应用，最早于 2027 年末推出，项目仍处早期阶段。同一报道称，苹果在 macOS 27.3 中加入警告页，使第三方智能体获取 Mac 控制权限的步骤从 4 步增加到 14 步；据报道，Meta Muse、OpenAI 等已推出同类智能体。上述内容来自招聘信息与媒体报道，苹果尚未公开确认该智能体产品，因此这属于早期研发计划的迹象，并非已经交付的能力。

telegram · zaihuapd · 11月20日 08:59

**「背景」** 主动式 AI 智能体指无需用户逐步下达指令，即可自行规划并执行多步任务的软件代理，通常涉及代码执行、网页浏览和应用控制等能力。苹果在 macOS 27.3 中把第三方智能体获取 Mac 控制权限的步骤从 4 步增加到 14 步，显示其在开放这类能力前先收紧权限门槛；Meta Muse、OpenAI 等已有同类智能体，构成苹果追赶的外部参照。

**「影响」** 对第三方智能体开发者而言，macOS 27.3 把获取 Mac 控制权限的流程从 4 步延长到 14 步并插入警告页，意味着现有自动化与代理类工具需要重新设计授权引导流程，用户实际配置成本随之上升；在苹果自研智能体最早 2027 年末才可能推出之前，第三方产品在 Mac 上仍需走这套更繁琐的授权路径。

**标签**: `#Apple`, `#AI agents`, `#macOS`, `#automation`, `#platform policy`

---

## 科技博客

<a id="item-tech-blog-1"></a>
### [输出缓存为何难以奏效](https://seangoedecke.com/why-output-caching-doesnt-work/) ⭐️ 6.0/10

rss · Sean Goedecke · 11月21日 00:00

**「背景」** LLM 的推理经济性通常依赖缓存输入，避免每轮重新计算整个对话历史；但模型也会在输出中重复内容，于是把缓存思路扩展到输出似乎顺理成章。作者指出，这种类比忽略了输出 token 的生成成本更高：输入可并行处理，输出只能逐个生成。

**「方案」** 输出确实常被浪费：代理会复述代码片段、引用证据文档或重放样例，而这些内容用户本可自己查看。作者设想通过提示或微调，让模型改输“src/script.py:12-15”这类引用，由执行框架展开，从而避免复述。但问题在于，这只能优化用户可见的输出；据作者对自己代理历史的观察，可见输出仅约占输出 token 的 6%，推理 token 占 50%，工具调用占 44%。按 Amdahl 定律，即便乐观地省掉可见输出三分之二的 token，总输出也只减少约 4%。因此真正要削减的是不可见的 94%，而这主要取决于模型智能：更强模型能用更少推理和工具调用得到正确答案，甚至可能出现单 token 贵 5 倍、总 token 少 6 倍因而总成本更低的情况。作者也承认，6% 来自个人经验且缺乏方法说明，前沿模型是否会在链式思考中重复只是推测。

**「启示」** 作者的结论是，输出缓存只瞄准可见输出这一小部分，受 Amdahl 定律限制，节省空间有限；优化 LLM 成本应关注推理与工具调用 token，并重视“更贵的模型可能整体更便宜”这一总成本视角。

**标签**: `#LLM inference economics`, `#output caching`, `#Amdahl&\#x27;s law`, `#agent token usage`, `#reasoning models`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [沃什避免前瞻指引，美联储官员却更频繁公开谈论加息](https://www.cnbc.com/2026/11/20/warsh-fed-forward-guidance-rate-hikes.html) ⭐️ 7.0/10

美联储主席凯文·沃什上任六个月来刻意避免就利率路径提供前瞻指引，但其他官员正更频繁地公开讨论加息，美国银行分析称过去两周的“美联储讲话”为 2025 年初以来同期最多。据 CME Group 的 FedWatch，市场定价显示交易员认为 12 月至少加息 25 个基点的概率为 100%。

rss · CNBC Finance · 11月20日 21:10

**「背景」** 所谓“前瞻性指引”，是指央行提前向市场释放未来利率路径的信号；据媒体报道，沃什今年出任美联储主席后取消了这一做法，把政策声明压缩到 132 词，主张不让官员提前锁定决策（tool-1-1）。他此前还提出减少 FOMC 会议和公开表态等沟通改革设想（tool-1-3）。

**「影响」** 若 12 月加息兑现，负债成本与政策利率挂钩的消费者和企业将面临更高利息支出；美国银行还警告，公开争论正在加大本已动荡环境中的利率波动。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.financialexpress.com/market/global-market-pulse/why-fed-chair-warsh-scrapped-forward-guidance-in-a-132-word-pivot/4272071/">Why Fed Chair Warsh scrapped forward guidance in a 132-word ...</a></li>
<li><a href="https://cryptobriefing.com/fed-chair-warsh-communication-reforms/">Federal Reserve Chair Kevin Warsh proposes communication ...</a></li>

</ul>
</details>

**标签**: `#Federal Reserve`, `#monetary policy`, `#interest rates`, `#FOMC`, `#forward guidance`

---

<a id="item-finance-news-2"></a>
### [美国企业转向净发行股票，新增供给或成牛市逆风](https://www.cnbc.com/2026/11/20/equity-issuance-bull-market-problem.html) ⭐️ 7.0/10

据 Acadian Asset Management 本月致投资者的分析，截至上周晚些时候，美国公司净新股发行量相当于总市值的 3.1%，显示企业已从 2024 年的回购转向发行股票，尽管仍低于科技泡沫和疫情泡沫时期的高峰。

rss · CNBC Finance · 11月20日 14:15

**「背景」** 过去多年企业回购会减少可交易股票数量，并因分母缩小而抬高每股收益，这曾被一些投资者视为股价支撑；如今这一趋势逆转，Acadian 的 Owen Lamont 称问题在于“聪明钱”为何卖出。

**「影响」** 甲骨文、Meta 和 Alphabet 等今年已进行大额股权融资的公司，以及需要消化这些新增供给的投资者，可能面临 Acadian 所说的股票供给增加带来的潜在市场逆风。

**标签**: `#equity issuance`, `#buybacks`, `#bull market`, `#AI capex`, `#IPO market`

---

<a id="item-finance-news-3"></a>
### [北京拟规定租房正常损耗不得扣减押金](https://mp.weixin.qq.com/s/PmGxh5knIyxiBRhpRoJnoQ) ⭐️ 7.0/10

北京市住建委与市场监管局 11 月 20 日起就《北京市住房租赁合同（示范文本）（修订征求意见稿）》公开征求意见，拟明确承租人正常使用造成的房屋损耗不承担赔偿责任，出租人不得以此为由扣减押金；征求意见稿还要求从事转租经营的租赁企业将租金、押金付至监管账户。

telegram · zaihuapd · 11月20日 13:46

**「背景」** 示范文本是主管部门提供、供租赁双方参照签约的合同范本，并非强制条款。此前北京市住建委已联合市场监管局就规范个人“二房东”转租公开征求意见，此次修订把押金、租金监管要求进一步落到合同环节。

**「影响」** 若条款定稿，在北京按该示范文本签约的租户被以“正常损耗”为由扣押金的空间将收窄；从事转租经营的租赁企业则须把租金和押金放入监管账户，接受押金托管与租金监管。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://house.cnr.cn/rdtj/20250710/t20250710_527254499.shtml">北 京 加强个人“二 房 东” 监 管 促进 住 房 租 赁 市场健康发展_央广网</a></li>

</ul>
</details>

**标签**: `#北京住房租赁`, `#押金监管`, `#租户权益`, `#政策征求意见`, `#住房租赁市场`

---