---
layout: default
title: "Horizon Summary: 2026-11-20 (ZH)"
date: 2026-11-20
lang: zh
---

> 从 34 条内容中筛选出 11 条重要资讯。

---

**科技新闻**
1. [PostgreSQL 19 发布，新增 WAIT FOR LSN 保障备库读一致性](#item-tech-news-1) ⭐️ 9.0/10
2. [Anthropic 纳斯达克上市引发估值与软件工程职业争论](#item-tech-news-2) ⭐️ 8.0/10
3. [PHP 混合大小写 HTTPS 流包装器静默禁用 TLS](#item-tech-news-3) ⭐️ 8.0/10
4. [Anthropic 称 Claude 参与解决两个黑洞物理开放问题](#item-tech-news-4) ⭐️ 7.0/10
5. [欧盟委员会向逾 4 万名员工部署 Matrix](#item-tech-news-5) ⭐️ 7.0/10
6. [OpenJDK“java4shell”报告引发披露时序争议](#item-tech-news-6) ⭐️ 7.0/10
7. [英国政府被迫承认向 Apple 发出秘密加密命令](#item-tech-news-7) ⭐️ 7.0/10
8. [PHP 计划发布最高级别安全更新](#item-tech-news-8) ⭐️ 7.0/10
9. [OpenAI 称模型参与 Jalapeño 与 AMD GPU 设计](#item-tech-news-9) ⭐️ 7.0/10
10. [Gemini 为 Mac 增加电脑操作功能，支持后台运行与审批](#item-tech-news-10) ⭐️ 7.0/10

**财经新闻**
1. [Anthropic 上市后 AI 投资疑虑升温，亚洲股市普跌](#item-finance-news-1) ⭐️ 8.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [PostgreSQL 19 发布，新增 WAIT FOR LSN 保障备库读一致性](https://simonwillison.net/2026/Nov/19/postgresql-19/) ⭐️ 9.0/10

PostgreSQL 19 已发布，新增 WAIT FOR LSN 命令，让向备库发送读请求的应用实现“读己之写”一致性。会话可在备库上等待 WAL 重放到指定 LSN 后再执行查询，并可选用 TIMEOUT；若备库未在时限内追上则报错。该版本比通常的 9 月发布窗口晚约两个月，Simon Willison 称延期主要与团队忙于处理大量由 AI 报告的漏洞有关。

rss · Simon Willison · 11月19日 20:43

**「背景」** PostgreSQL 的流复制会把只读查询发送到 standby，而 standby 必须先重放主库写入的 WAL；在重放追平之前，查询可能读不到刚提交的数据。LSN 用于标记 WAL 中的位置，因此应用可以把主库返回的 LSN 带到 standby 上等待重放，这是实现“读到自己刚写的数据”的前提。另一个背景是，PostgreSQL 通常每年 9 月发布大版本，而 19 版此次推迟到 11 月，原文作者称主要原因是团队需要处理大量由 AI 报告的漏洞问题。

**「影响」** 对使用只读备库的开发者而言，可在写入后保存主库返回的 LSN，在后续请求中先对备库执行 WAIT FOR LSN 再查询，从而避免因复制延迟读到旧数据；代价是应用需要传递该 LSN，并处理等待超时错误。

**标签**: `#PostgreSQL`, `#database release`, `#WAIT FOR LSN`, `#WAL replication`, `#read consistency`

---

<a id="item-tech-news-2"></a>
### [Anthropic 纳斯达克上市引发估值与软件工程职业争论](https://www.reuters.com/business/finance/anthropics-historic-debut-put-ais-promise-peril-wall-st-test-2026-11-19/) ⭐️ 8.0/10

Anthropic 登陆纳斯达克，Hacker News 的讨论焦点随即落在其估值和软件工程岗位前景上。评论中引用的交易数据显示，该股 IPO 定价为 83 美元，开盘 111.5 美元，收盘 97.17 美元：较发行价上涨 17.07%，但较开盘价下跌 12.85%，对应约 1.26 万亿美元估值。上述数字来自社区评论而非已核实的行情数据；讨论还提到，几周前市场曾期待 2 万亿美元以上的估值。

hackernews · wslh · 11月19日 17:02 · [社区讨论](https://news.ycombinator.com/item?id=50562754)

**「背景」** IPO 是公司首次向公众发行股票并在交易所挂牌：发行价在上市前确定，开盘后的价格则由公开市场交易决定。对 Anthropic 而言，纳斯达克上市意味着其估值不再只由私募融资轮次体现，而会接受公开市场的每日定价；首日发行价、开盘价与收盘价之间的差距，也放大了市场对 AI 公司估值的分歧。

**「社区讨论」** 评论区最实质的争论是 AI 是否正在终结软件工程的“轻松赚钱”时代：有资深开发者说自己从业 50 年，过去公司会全额资助去学 C 语言，如今却很难给新人建议；也有评论用同日股价“较发行价涨 17.07%、较开盘价跌 12.85%”来论证估值叙事已降温，并认为这对 OpenAI 的私募估值不是好兆头。

**标签**: `#Anthropic`, `#AI industry`, `#IPO`, `#software engineering jobs`, `#valuations`

---

<a id="item-tech-news-3"></a>
### [PHP 混合大小写 HTTPS 流包装器静默禁用 TLS](https://x.com/ljachowicz/status/2123477025268924514) ⭐️ 8.0/10

PHP 已修复一个流包装器漏洞：HTTP/FTP 的 scheme 识别不区分大小写，但只有第五个字符为小写 s 时才启用 TLS。据报告，HTTPS://、httpS:// 和 FTPS:// 因此会被当作明文 HTTP/FTP 发送，可能暴露令牌、Basic 认证信息、Cookie、POST 请求体和 FTP 登录信息，第三方重定向到这类地址也会触发。漏洞编号为 CVE-2026-128064（GHSA-f6gg-rchx-xw8j），CVSS 4.0 评分 8.2；PHP 8.2.36、8.3.37、8.4.28、8.5.13 和 8.6.0 已修复，8.1 及更早版本已 EOL、不会修复。这些旧版本的用户只能自行把 URL 的 scheme 统一转为小写。

telegram · zaihuapd · 11月20日 03:04

**「背景：scheme 解析」** PHP 的 HTTP/FTP 流包装器在识别 URL scheme 时不区分大小写，但启用 TLS 时只检查固定位置是否为小写 s。这种解析与 TLS 判断的不一致，正是混合大小写地址可能落入明文传输的前提。PHP 8 的变更日志已将 GHSA-f6gg-rchx-xw8j（CVE-2026-128064）列为修复项。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://everycve.com/CVE-2026-128064">CVE - 2026 - 128064 : Mixed-case HTTPS and FTPS URLs can expose...</a></li>
<li><a href="https://www.php.net/ChangeLog-8.php">PHP : PHP 8 ChangeLog</a></li>

</ul>
</details>

**标签**: `#PHP`, `#TLS`, `#security vulnerability`, `#CVE`, `#web security`

---

<a id="item-tech-news-4"></a>
### [Anthropic 称 Claude 参与解决两个黑洞物理开放问题](https://www.anthropic.com/research/claude-black-hole-physics) ⭐️ 7.0/10

Anthropic 发布研究公告，声称 Claude 参与解决了两个黑洞物理的开放理论问题；这是厂商自述，目前没有独立验证。公告称，这两项结果都不直接描述我们的宇宙，也没有实际应用，而是服务于量子力学与广义相对论统一的长线理论工作。公告没有说明使用了什么提示词，也没有提供可复核的贡献边界，因此当前能确认的是 Anthropic 提出了这一主张，而非 Claude 已作为独立研究者完成证明。

hackernews · cybermango · 11月19日 17:30 · [社区讨论](https://news.ycombinator.com/item?id=50563148)

**「背景」** 这项结果出自 Anthropic 为 Claude Fable 5.2 发布准备的研究材料：相关页面以“Claude Fable 5.2 solves two open problems in…”为题，把两篇论文（其中一篇围绕 modular bootstrap，即模自举方法）作为该模型的研究成果展示，而非同行评审的期刊发表。因此读者面对的是厂商自述的能力展示，公告并未交代模型在其中获得的具体提示与人工参与程度。

**「影响」** 对量子引力研究者而言，这两项结果目前的价值限于理论约束：公告称其中一项结果给出了检验候选量子引力理论所用某种最简方法的确切上限，可用于排除超出该上限的候选理论；但公告也明确说明两项结果都不直接描述我们所在的宇宙，且没有实际应用。另一个直接后果是可核查性：有评论者指出公告与两篇论文中都没有出现“prompt”一词，在提示词与人工介入程度公布之前，外部研究者难以复现结果，也难以界定模型在其中承担了多少工作。

**「社区讨论」** 讨论中最集中的质疑是拟人化：dap 认为“Claude solves”掩盖了提示词与实际贡献方式，并指出公告、摘要和两篇论文里都没有出现“prompt”。chunky1994 则把第二项结果视为更有分量的贡献，称其证明黑洞质量存在与给定中心电荷一致的上限，从而使相应理论成为自洽的量子引力理论；这些判断目前都来自评论者，而非独立复核。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.anthropic.com/research/claude-black-hole-physics">Claude Fable 5.2 solves two open problems in the physics of black ...</a></li>
<li><a href="https://www.anthropic.com/research/claude-black-hole-physics">Claude Fable 5.2 solves two open problems in the physics of black ...</a></li>

</ul>
</details>

**标签**: `#AI for science`, `#theoretical physics`, `#black holes`, `#Claude`, `#AI research`

---

<a id="item-tech-news-5"></a>
### [欧盟委员会向逾 4 万名员工部署 Matrix](https://element.io/blog/how-the-european-commission-rolled-out-matrix-to-more-than-40-000-staff/) ⭐️ 7.0/10

Element 的博客文章介绍了欧盟委员会向超过 4 万名员工部署 Matrix 的情况，这是一次大规模开源联邦通信系统落地。现有材料没有提供部署时间表、所用客户端、加密配置或独立性能数据，因此具体技术细节仍无法核实。文章来自 Matrix 生态厂商 Element，读者应将其视为供应商叙述，而非独立评估。

hackernews · liotier · 11月19日 10:58 · [社区讨论](https://news.ycombinator.com/item?id=50558533)

**「背景：Matrix 协议与部署时间线」** Matrix 是一个开放、可联邦的去中心化通信协议，机构可以自行托管服务器，并与外部 Matrix 网络互通；Element 提供基于该协议的主要客户端与企业服务。据 Element 发布的部署说明，欧委会从 2025 年 12 月的原型起步，到 2026 年 9 月完成在笔记本电脑上的安装，历时约九个月，并将这套自托管系统与员工日常使用的 EU Login 登录体系打通。

**「影响」** 对考虑类似部署的公共机构而言，需要核实的兼容性事项包括客户端选择、端到端加密状态和运维支持；这些信息未在现有材料中披露。

**「社区讨论」** 评论者对 Matrix 的加密成熟度分歧明显：一位评论者称其端到端加密远未达到国家安全用例要求，并认为迁往 MLS 的工作似乎已停滞；另有日常用户肯定自托管带来的隐私和对实时位置共享的控制。还有用户抱怨客户端碎片化、会话验证和加密错误等问题，并希望欧盟委员会的采用能推动改进。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://element.io/blog/how-the-european-commission-rolled-out-matrix-to-more-than-40-000-staff/">How the European Commission rolled out Matrix to more than 40 , 000 ...</a></li>
<li><a href="https://dzen.ru/b/av7xwZrWnjnx2lAj">Еврокомиссия развернула Matrix на всех служебных... | Дзен</a></li>

</ul>
</details>

**标签**: `#Matrix`, `#open source`, `#public sector`, `#end-to-end encryption`, `#enterprise deployment`

---

<a id="item-tech-news-6"></a>
### [OpenJDK“java4shell”报告引发披露时序争议](https://github.com/openjdk/jdk/pull/32781) ⭐️ 7.0/10

OpenJDK 的 PR \#32781 提交了一份被称为“java4shell”的疑似安全漏洞报告，使 Java 用户和 OpenJDK 维护者面对一个尚无确认严重级别、受影响版本或官方公告的问题。评论中引用的 Adoptium 支持 issue 称，PR 作者 10 月 1 日表示 Oracle 要求其在获批前不要推进 PR，10 月 28 日又称此事已由 Oracle 接管；这些说法来自讨论，并非已发布的官方结论。现有材料不足以确认该问题是否真实可利用、影响哪些版本，或最终以何种方式修复。

hackernews · notmine1337 · 11月19日 11:47 · [社区讨论](https://news.ycombinator.com/item?id=50558906)

**「背景」** Java4shell 指 OpenJDK Base64 解码中的一个严重漏洞，Cisco Talos 以 CVE-2026-114938 跟踪，给出 CVSS 4.0 9.2 分，并称其可能导致未认证远程代码执行；SOC Prime 也将其描述为可引发内存破坏、崩溃和 RCE 的缺陷。此次 OpenJDK PR 就是围绕该 Java4shell 报告及修复展开的，讨论中的评论还称 Oracle 曾要求报告者暂缓提交 PR、随后接管处理。

**「影响范围与处置」** 外部厂商分析将 java4shell 标为 CVE-2026-114938，并称受影响的是基于 OpenJDK 17.0.6 及以后构建、运行在支持 AVX-512 VBMI 的 x86-64 平台上的 Java 环境；因此运维团队应先盘点 JDK 构建版本和主机 CPU 特性，再迁移到修复构建，而不能只按 Java 主版本判断是否安全。

**「社区讨论」** 评论者对发现来源看法不一：有人怀疑辅助研究的大模型可能读过此前的公开报告，而非独立发现；一位自称提前发现并报告 Oracle 的用户称其工具离线运行、无法直接访问该 PR，但承认不能排除训练数据污染，并认为同时披露如今很常见。另有评论认为，判断漏洞严重性并构建利用链仍需人工监督，因此不应把模型辅助等同于完整自主发现。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://blog.talosintelligence.com/java4shell/">CVE-2026-114938: Critical vulnerability in OpenJDK Java</a></li>
<li><a href="https://socprime.com/blog/cve-2026-114938-java4shell-flaw-enables-pre-auth-rce-in-major-java-applications/">CVE-2026-114938: Java 4 Shell RCE Vulnerability</a></li>
<li><a href="https://orca.security/resources/research/java4shell-critical-openjdk-base64-decoder-flaw-could-allow-unauthenticated-remote-code-execution/">Java 4 Shell CVE-2026-114938: Affected Versions &amp; Mitigation</a></li>
<li><a href="https://blog.talosintelligence.com/java4shell/">CVE-2026-114938: Critical vulnerability in OpenJDK Java</a></li>
<li><a href="https://www.cyberkendra.com/2026/11/cve-2026-114938-pre-auth-rce-flaw-in-java-17-puts-servers-at-risk.html">Java 4 Shell (CVE-2026-114938): Affected Versions , Fix, Workaround</a></li>

</ul>
</details>

**标签**: `#Java security`, `#OpenJDK`, `#vulnerability disclosure`, `#AI-assisted security research`

---

<a id="item-tech-news-7"></a>
### [英国政府被迫承认向 Apple 发出秘密加密命令](https://macanorak.com/uk-government-forced-to-admit-it-issued-apple-a-secret-encryption-order/) ⭐️ 7.0/10

英国政府被迫承认曾向 Apple 发出一项秘密加密命令，相关命令的具体内容仍未公开。事件的核心争议在于政府监控权限、加密后门风险，以及厂商安全承诺是否仍然可信。对 Apple 用户和企业客户来说，关键在于这项命令要求 Apple 提供何种技术协助，但目前公开信息不足以确认。

hackernews · Terretta · 11月19日 16:21 · [社区讨论](https://news.ycombinator.com/item?id=50562113)

**「背景」** 英国《2016 年调查权力法》第 253 条允许内政大臣向“相关运营商”发出技术能力通知（TCN），要求其维持让情报机构获取用户数据的能力。2025 年 4 月 7 日的调查权力法庭（IPT）判决曾记录，媒体已广泛报道英国政府签署了一项 TCN，要求 Apple 保持向情报机构提供解密形式用户数据的能力；2026 年 11 月 19 日的 IPT 判决则直接处理 Apple 对内政大臣等方的挑战，并审查内政大臣发出 TCN 的权力。

**「影响」** 在命令内容保密的情况下，Apple 用户和企业客户无法独立核实其安全承诺是否仍能排除政府获取数据的途径；依赖 Apple 加密服务的组织应把供应商合规披露和司法辖区风险纳入评估。

**「社区讨论」** 评论者 natch 认为 Apple 的安全表述已从“连 Apple 也无法访问”弱化为“Apple 无法访问”，并称设备上的密钥可能只是用于解开实际数据密钥的 KEK；fweimer 指出，相关裁决显示媒体是通过机密安全简报而非泄密获知该通知，内容仍未公开。另有评论者批评英国在西方国家标准下仍公开、强硬地扩张监控。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://investigatorypowerstribunal.org.uk/judgement/1-mr-vincent-kearney-2-british-broadcasting-corporation-v-1-chief-constable-of-the-police-service-of-northern-ireland-2-chief-constable-of-durham-constabulary-3-security-service-4-governme/">Apple Inc and Secretary of State for the Home Department and ...</a></li>
<li><a href="https://www.judiciary.uk/judgments/apple-inc-v-home-secretary-and-others/">Apple Inc -v- Home Secretary and others - Courts and ...</a></li>
<li><a href="https://investigatorypowerstribunal.org.uk/judgement/apple-inc-v-secretary-of-state-for-the-home-department/">Apple Inc v Secretary of State for the Home Department</a></li>

</ul>
</details>

**标签**: `#encryption`, `#UK surveillance`, `#Apple`, `#privacy policy`, `#technical capability notice`

---

<a id="item-tech-news-8"></a>
### [PHP 计划发布最高级别安全更新](https://www.php.net/archive/2026.php) ⭐️ 7.0/10

PHP 安全团队宣布计划于 2026 年 11 月 19 日 UTC 14:00 至 14:30 发布安全更新，修复影响所有受支持 PHP 版本、最高严重级别为 CRITICAL 的漏洞。该更新属于每四周一次的常规发布周期；官方称 CRITICAL 问题只在非默认配置或不常见环境下触发。具体技术细节和修复版本号将在更新发布时一并公布，目前尚未披露 CVE 编号或修复版本。

telegram · zaihuapd · 11月19日 07:10

**「背景」** PHP 安全团队按每四周一次的固定节奏发布安全更新，并会在正式上线前先发出预告。此次预告将最高严重级别标为 CRITICAL，但说明该问题只在非默认配置或不常见环境下触发，具体技术细节和修复版本号要等到 11 月 19 日 UTC 14:00 至 14:30 的发布窗口才公布。

**「影响」** 使用受支持 PHP 版本的用户应在更新上线后尽快升级；但在 CVE 编号、修复版本号和触发条件公布前，管理员还无法判断自身部署是否受影响，只能先关注发布并准备升级。

**标签**: `#PHP`, `#security advisory`, `#critical vulnerability`, `#open-source software`

---

<a id="item-tech-news-9"></a>
### [OpenAI 称模型参与 Jalapeño 与 AMD GPU 设计](https://openai.com/index/advancing-chip-design-with-our-models/) ⭐️ 7.0/10

OpenAI 表示，其模型参与了自研推理芯片 Jalapeño 的设计：向量单元的标准单元面积减少约 13%，矩阵单元减少约 10%，相关优化已在芯片点亮中验证。OpenAI 还称，在与 AMD 的合作中，其模型帮助旗舰 GPU IP 的功耗、性能、面积（PPA）指标相比高度优化的基线提升最高 14%，部分改动已进入送厂制造的设计。OpenAI 同时宣布与 Synopsys 合作训练 GPT-Synopsys 模型。上述数据均为 OpenAI 公布的公司口径，现有信息未提供可独立复核的基准或完整技术细节。

telegram · zaihuapd · 11月19日 09:30

**「背景」** 芯片设计中的 PPA（功耗、性能、面积）与标准单元面积是衡量电路实现优劣的核心指标，面积缩小通常意味着同等工艺下更低的成本与更高的集成度。OpenAI 与 Synopsys 的合作已于 2026 年 9 月 30 日宣布，按披露条款，OpenAI 向 Synopsys 支付训练订阅费，让模型学习使用其工具，待 Synopsys 客户采用后，双方再按模型对芯片设计的改进程度分成（tool-2-2、tool-2-3）；本次报道为这一合作以及 OpenAI 自研 Jalapeño 推理芯片给出了可量化的设计结果。

**「影响」** 对芯片设计团队而言，可以评估将大模型用于标准单元面积和 PPA 优化，尤其是针对已经高度优化的基线；但在把模型建议送入制造前，仍需用自有工艺库、签核流程和独立基准进行验证，当前 13%、10% 和最高 14% 的收益不能直接外推。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://yage.ai/share/ai-agent-pipelines-pricing-en-20261007.html">OpenAI Pays to Learn Chip Tools, an AI Agent Starts Emailing...</a></li>
<li><a href="https://www.taylortailored.co.uk/science-technology-1/openai-is-building-an-ai-that-designs-computer-chips-and-the-feedback-loop-could-be-enormous">OpenAI Chip Design: How The AI Feedback Loop... | Taylor Tailored</a></li>

</ul>
</details>

**标签**: `#AI for chip design`, `#OpenAI`, `#AMD`, `#Synopsys`, `#semiconductor hardware`

---

<a id="item-tech-news-10"></a>
### [Gemini 为 Mac 增加电脑操作功能，支持后台运行与审批](https://www.bloomberg.com/news/articles/2026-11-19/google-s-gemini-can-now-control-mac-devices-on-users-behalf) ⭐️ 7.0/10

彭博社报道，Google Gemini 在 Mac 版应用中新增“电脑操作”功能，可代用户点击、输入、浏览菜单和填写表单。该功能已向美国地区订阅 Google AI Plus、Pro 或 Ultra 的 Mac 版 Gemini 用户开放；Gemini 可在独立后台窗口运行，用户仍可继续使用主屏幕和光标。用户可限制它能访问的应用、实时查看操作、随时暂停，并在关键操作前进行审批；现有信息未提供独立测试或更细的性能数据。

telegram · zaihuapd · 11月20日 02:51

**「背景」** 桌面代理指的是让模型直接在图形界面中点击、输入并跨应用完成多步骤任务，而不只是生成文本回答。Bloomberg 在报道此次更新时指出，其他主流 AI 助手已提供类似的电脑控制能力，Gemini 的 Mac 版本是在追赶这一方向，并因此加大了对 Apple 的压力。

**「影响」** 对符合条件的用户，重复的点击和表单流程可交给后台代理执行，而不必让出主屏幕；实际使用时仍需先收紧可访问应用范围，并对关键操作保留审批，以降低代理误触敏感流程的风险。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.bloomberg.com/news/articles/2026-11-19/google-s-gemini-can-now-control-mac-devices-on-users-behalf">Google’s Gemini Can Now Control Mac Devices on Users’ Behalf</a></li>

</ul>
</details>

**标签**: `#AI agents`, `#Google Gemini`, `#desktop automation`, `#macOS`, `#user controls`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [Anthropic 上市后 AI 投资疑虑升温，亚洲股市普跌](https://www.bloomberg.com/news/articles/2026-11-19/stock-market-today-dow-s-p-live-updates) ⭐️ 8.0/10

Anthropic 上市后股价盘后跌逾 5%、跌破 92 美元，引发市场对 AI 巨额投入回报的疑虑，亚洲股市随之走弱：MSCI 亚太指数跌 1.7%，为连续第七个交易日下跌；韩国 Kospi 指数跌 3.66%，三星电子跌 4.7%、SK 海力士跌 6%，东京电子跌 7.19%。软银已累计向 OpenAI 投资 646 亿美元，其股价 10 月下跌 30%，本月又跌 31%。

telegram · zaihuapd · 11月20日 01:58

**「背景」** Anthropic 此次上市在 11 月 12 日前后获彭博报道称认购达六倍超额，市场此前因此对 AI 投资主题情绪偏乐观；如今其股价在上市后跌破 92 美元，投资者开始重新审视 AI 巨额投入能否带来相应回报。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.marketpulse.com/markets/anthropics-ipo-a-make-or-break-test-for-the-trillion-dollar-ai-trade/">Anthropic’s IPO: A make-or-break test for the trillion-dollar ...</a></li>

</ul>
</details>

**标签**: `#AI investment`, `#Asian equities`, `#semiconductor stocks`, `#market selloff`, `#SoftBank/OpenAI`

---