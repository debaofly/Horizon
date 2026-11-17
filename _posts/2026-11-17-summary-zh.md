---
layout: default
title: "Horizon Summary: 2026-11-17 (ZH)"
date: 2026-11-17
lang: zh
---

> 从 48 条内容中筛选出 15 条重要资讯。

---

**科技新闻**
1. [vLLM v0.34.0 发布：KV 缓存默认扩展、移除 Model Runner V1](#item-tech-news-1) ⭐️ 8.0/10
2. [Jiff 1.0 发布：Rust 日期时间库进入稳定版](#item-tech-news-2) ⭐️ 8.0/10
3. [美商务部将 AI 芯片管制扩至远程访问](#item-tech-news-3) ⭐️ 8.0/10
4. [卡内基梅隆大学在 YouTube 免费发布整学期计算机课程](#item-tech-news-4) ⭐️ 7.0/10
5. [Windows 11 被指遥测收集编程代理与开发工具信息](#item-tech-news-5) ⭐️ 7.0/10
6. [微软称大规模邮件中断源于 7 月修复引入的缺陷](#item-tech-news-6) ⭐️ 7.0/10
7. [Optimizely 据报遭入侵，经 Zoom 和 GitLab 等站点投放恶意代码](#item-tech-news-7) ⭐️ 7.0/10
8. [Marimba：单次冻结 ASR 编码器复用多任务语音查询](#item-tech-news-8) ⭐️ 7.0/10
9. [Duetto 不微调，用采样时 logit 引导实时爵士伴奏](#item-tech-news-9) ⭐️ 7.0/10
10. [美与九国签署《旧金山宣言》共保超级智能供应链](#item-tech-news-10) ⭐️ 7.0/10
11. [阿里等中国 AI 公司据报收紧新模型网络攻击能力](#item-tech-news-11) ⭐️ 7.0/10
12. [Xbox 确认 Project Helix 是可玩 PC 游戏的主机](#item-tech-news-12) ⭐️ 7.0/10

**财经新闻**
1. [英伟达 CEO 辞职、国会易主：ETF 专家谈 AI 交易可能如何变化](#item-finance-news-1) ⭐️ 7.0/10
2. [卢特尼克因英伟达相关关系受质疑，其子执掌的坎托减持英伟达](#item-finance-news-2) ⭐️ 7.0/10
3. [英特尔及 CEO 陈立武遭股东集体诉讼](#item-finance-news-3) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [vLLM v0.34.0 发布：KV 缓存默认扩展、移除 Model Runner V1](https://github.com/vllm-project/vllm/releases/tag/v0.34.0) ⭐️ 8.0/10

vLLM 发布 v0.34.0，包含 1,061 次提交、412 名贡献者。该版本在 CUDA 和 ROCm 上默认启用可扩展 KV 缓存，按预热后实际空闲显存确定容量；同时移除 Model Runner V1，默认块大小从 16 改为 64，ROCm 仅提供 10.0 构建，并要求 huggingface\_hub &gt;= 2.0.0。发布说明称新版本新增 Mistral Large 4、MiniMax-M3.1-Flash、Nemotron-3.5-Transcribe 等 10 个模型，并在 Blackwell 和 MI355X 上取得最高 1.95 倍解码等提升。

github · khluu · 11月16日 23:22

**「背景」** vLLM 是面向大模型推理的服务引擎，KV 缓存用于保存注意力计算中的键值状态，其容量会直接影响并发吞吐和首 token 延迟。此前版本同时保留 Model Runner V1 和 V2 两套 GPU 执行路径，默认块大小为 16，KV 缓存容量主要依赖预热前的估算。v0.34.0 将执行路径收敛为 MRV2，把默认块大小改为 64，并改为按预热后实际空闲显存确定缓存大小。

**「影响」** 升级方需移除 VLLM\_USE\_V2\_MODEL\_RUNNER=0（否则启动失败），并检查旧日志处理器、块大小和相关量化配置；若要维持旧缓存策略，可传 --gpu-memory-utilization 0.9 或 --no-enable-extensible-kv-cache。发布说明还提示默认缓存策略虽提高高并发吞吐，却可能让部分 H200 模型在并发 128 时 TPOT 增加 6–18%。

**标签**: `#vLLM`, `#LLM inference`, `#KV cache`, `#model runner`, `#performance`

---

<a id="item-tech-news-2"></a>
### [Jiff 1.0 发布：Rust 日期时间库进入稳定版](https://burntsushi.net/jiff/) ⭐️ 8.0/10

Jiff 1.0 正式发布，这是 burntsushi 开发的 Rust 日期时间库的首个稳定版本，面向 Rust 生态中需要处理日期和时间的开发者。现有材料没有说明 1.0 的具体 API 变更、性能数据或兼容性范围；评论中引用的项目文档也提醒，Jiff 并非所有场景都适用。

hackernews · burntsushi · 11月16日 16:53 · [社区讨论](https://news.ycombinator.com/item?id=50519744)

**「背景」** Jiff 是 burntsushi 开发的 Rust 日期时间库，此次发布的 1.0 是该库的首个稳定版本。Rust 生态中长期由 chrono 承担日期时间处理；讨论中一位自称维护 chrono 约五年的用户表示，chrono 的 API 之所以难有改动，是因为使用者看重其稳定性，任何改进尝试都会遇到阻力——这为理解 Jiff 为何在既有生态之外重新设计接口提供了背景。

**「对 Rust 项目的影响」** 对 Rust 开发者来说，1.0 版本意味着新项目可以基于一个 API 已稳定的日期时间库编写代码；但已经深度使用 chrono 的项目需要权衡迁移成本，因为 Jiff 文档明确说明它并非所有场景都适用。社区中一位曾长期维护 chrono 的开发者指出，既有库的 API 稳定性恰恰是用户不愿更换的原因，这预示着生态采用会更偏向新项目，而不是大规模迁移。

**「社区讨论」** 一位自称维护 chrono 约五年的评论者说，chrono 的 API 稳定性是用户依赖它的原因，但也让改进屡遇阻力，他因难以推进改进而停止维护，同时仍感谢 burntsushi 开发新的日期时间库；另有评论者赞赏 Jiff 明确说明自己并非适用于所有场景，并希望生态更多采用它。

**标签**: `#Rust`, `#datetime`, `#libraries`, `#open source`, `#API design`

---

<a id="item-tech-news-3"></a>
### [美商务部将 AI 芯片管制扩至远程访问](https://www.reuters.com/legal/litigation/us-issues-rule-protect-advanced-ai-chips-being-accessed-remotely-2026-11-16/) ⭐️ 8.0/10

美国商务部于 11 月 16 日发布临时最终规则，将先进 AI 芯片和服务器的出口管制延伸到远程访问，以堵住通过第三国数据中心规避限制的路径。规则还要求向印度尼西亚、马来西亚、新加坡、泰国和巴西再出口 AI 芯片时申请许可。报道认为，这可能进一步收紧中国获取先进芯片的渠道。来源未说明规则的具体技术门槛、生效日期或执行细节，实际适用范围仍待明确。

telegram · zaihuapd · 11月16日 14:44

**「背景：出口管制为何盯上“远程访问”」** 美国对先进 AI 芯片与服务器的出口管制，传统上针对的是货物本身的出口、再出口和跨境转移，由商务部工业与安全局（BIS）依据出口管理条例（EAR）执行。这类管制以芯片或服务器的物理流向为对象，而境外数据中心只要不转手硬件、仅以云服务形式把算力“租”给受限地区的用户，就可能落在规则文本之外。此次新规把远程访问纳入管制范围，正是针对这一存在于第三国数据中心的路径。

**「对云服务商与跨境算力用户的影响」** 在新加坡、马来西亚、印度尼西亚、泰国和巴西运营数据中心或提供云端 AI 算力的企业，向这些地点再出口先进 AI 芯片前必须先申请许可，因此相关云服务商需要在规则落地前重新梳理供货路径与算力部署方案。依赖跨境远程调用美国芯片算力的开发者同样面临合规不确定性：若相关访问未获许可，原有调用方式可能无法延续，需提前评估替代算力来源。该规则为临时最终规则，源材料未披露具体许可条件与生效时间。

**标签**: `#AI chips`, `#export controls`, `#US policy`, `#semiconductors`, `#cloud computing`

---

<a id="item-tech-news-4"></a>
### [卡内基梅隆大学在 YouTube 免费发布整学期计算机课程](https://www.cs.cmu.edu/learn/) ⭐️ 7.0/10

卡内基梅隆大学格里芬计算机科学学院的 CS Learn 已上线，开始在 YouTube 免费发布当前 CMU 计算机科学课程的整学期讲座，本周每天首播一门，更多课程计划于明年 1 月加入。项目负责人 Phillip Compeau 表示，部分学生开发了自动化制作工具，让小团队也能承担大量课程制作；课程配套材料（courseware）也在计划中。现阶段公布的是视频课程资源，未提及学分、作业批改或结业认证。

hackernews · pcompeau · 11月16日 20:43 · [社区讨论](https://news.ycombinator.com/item?id=50522980)

**「背景：开放课程与自动化生产」** 开放课程（open courseware）是指高校把课程讲座、讲义等教学材料公开上网、免费供人使用，MIT 的 OpenCourseWare 是这一模式最早的大规模实践；CMU 的 Phillip Compeau 在讨论区中也承认“MIT 25 年前就已经做了”。此次与以往不同的是制作方式：Compeau 表示，几名学生开发了自动化工具，把大量制作环节自动化，因此一个小团队也能产出整学期的课程。

**「影响」** 对自学者来说，可以按 CMU 现有课程的完整讲座顺序免费学习；但首批资源以视频为主，项目、练习和反馈要依赖尚未发布的 courseware，因此不能据此视为可替代在校课程或获得学分。

**「社区讨论」** 评论中，CMU 校友对 15-259 概率与计算、Tianqi Chen 的 ML Systems 等课程表示期待；也有人强调讲座之外还需要项目与反馈，并希望课程库不只包含入门课而漏掉研究生阶段的编译器课程。另有评论认为，在 AI 时代打好基础能让 AI 成为工具，但这属于个人观点。

**标签**: `#computer science education`, `#open courseware`, `#online learning`, `#CMU`, `#ML systems`

---

<a id="item-tech-news-5"></a>
### [Windows 11 被指遥测收集编程代理与开发工具信息](https://xusheng.dev/posts/windows-coding-agent-telemetry/) ⭐️ 7.0/10

一篇开发者报告称，Windows 11 会收集开发者使用哪些编程代理和开发工具的信息，把这类使用情况纳入遥测，引发对开发者隐私和平台治理的讨论。评论转述称，在“可选诊断数据”开启（默认开启）时，这类开发工具数据可能被发送，关闭路径为“设置 → 隐私和安全性 → 诊断和反馈”。这些具体范围和默认状态目前来自报道及评论，尚无独立核验的微软说明。

hackernews · cwaffles · 11月16日 22:58 · [社区讨论](https://news.ycombinator.com/item?id=50524736)

**「背景」** Windows 11 的诊断数据分为“必需”和“可选”两层：必需数据包括设备标识、配置和基本健康信号，微软称这些数据为安全与核心运行所必需；可选诊断数据则涵盖更细的使用情况。用户可以在“设置 → 隐私和安全性 → 诊断和反馈”中关闭“发送可选诊断数据”，此次报道所涉及的开发工具遥测就属于这一可关闭的可选层级。

**「对开发者的实际影响」** 对使用 Windows 11 的开发者来说，直接后果是：所用编码代理和开发工具的名称可能随诊断数据一并上报，而这一行为取决于“诊断和反馈”中的遥测级别——有评论者指出该级别默认开启，关闭路径为“设置 → 隐私和安全性 → 诊断和反馈”。因此，需要在公司设备或标准镜像上约束工具使用信息外泄的团队，应显式调整这一设置，而不是依赖默认值。

**「社区讨论」** 有评论认为，Windows 更紧迫的问题是尽快提供 AI 代理沙箱：他们称微软的 MXC 才在 10 月 7 日推出、Claude Code 尚未支持，开发者目前只能运行未沙箱化代理或转用 WSL，因此非侵入式遥测可用来确定优先级。另一些评论把此事与显卡驱动收集可执行文件名和路径、Chrome 保存浏览历史、Debian popularity-contest 类比，强调应关注退出选项与透明度。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://windowsforum.com/windows-news.4/reduce-windows-11-telemetry-by-disabling-optional-diagnostic-data.382005/">Reduce Windows 11 Telemetry by Disabling Optional Diagnostic Data</a></li>
<li><a href="https://wccftech.com/how-to/disable-the-telemetry-on-windows-11-and-stop-microsoft-from-logging-your-data/">How to Disable Telemetry on Windows 11 and Protect Data Privacy</a></li>

</ul>
</details>

**标签**: `#Windows 11`, `#telemetry`, `#privacy`, `#AI coding agents`, `#developer tools`

---

<a id="item-tech-news-6"></a>
### [微软称大规模邮件中断源于 7 月修复引入的缺陷](https://www.theregister.com/saas/2026/11/16/microsoft-blames-monster-email-outage-on-software-defect-introduced-in-july-fix/5310026) ⭐️ 7.0/10

微软将一次大规模电子邮件服务中断归因于 7 月的一次修复引入的软件缺陷。相关报道没有提供受影响的具体服务名称、中断持续时间或用户规模，也没有说明是否已有永久修复；因此目前可确认的是微软的归因，而非经独立验证的根因。对依赖其托管邮件服务的用户来说，这是一次由后续变更触发的回归故障。

hackernews · Bender · 11月16日 13:18 · [社区讨论](https://news.ycombinator.com/item?id=50517321)

**「背景」** 据 NPR 报道，Outlook 在 11 月 12 日（周四）出现广泛中断，持续超过 12 小时，微软到次日凌晨才报告“有限恢复”。据 cybersecuritynews 梳理的事故报告，问题来自一项专为 Microsoft 365 网络网关服务器准备的修复，该变更于 7 月开始部署，并在全球运行三个多月未见异常。

**「影响」** 对依赖微软托管邮件服务的组织来说，直接后果是供应商侧的变更管理缺陷被列入业务连续性风险：在微软公布根因、永久修复和恢复细节之前，客户无法从现有报道判断同类故障是否会再次发生。

**「社区讨论」** 评论者从恢复策略和测试覆盖两个方向提出质疑：有人用电网“黑启动”类比说明大规模服务不能直接满载重启，也有人追问为何不通过限制连接或分片放量来降低负载。另有评论者对关键网络基础设施使用 Windows 表示意外，并指出低规格测试环境可能无法复现生产环境的并发缺陷。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.npr.org/2026/11/12/nx-s1-6039343/outlook-down-widespread-outage-microsoft-email">A negative Outlook: Microsoft scrambles to fix email outage : NPR</a></li>
<li><a href="https://cybersecuritynews.com/microsoft-outage-incident-report/">Microsoft Reveals How a Hidden Windows Bug Took Down Microsoft ...</a></li>

</ul>
</details>

**标签**: `#Microsoft`, `#service outage`, `#software regression`, `#incident response`, `#infrastructure reliability`

---

<a id="item-tech-news-7"></a>
### [Optimizely 据报遭入侵，经 Zoom 和 GitLab 等站点投放恶意代码](https://blog.report-uri.com/worlds-largest-brands-infected-with-malware-via-optimizely/) ⭐️ 7.0/10

据报，网页优化服务 Optimizely 遭入侵，并通过其客户网站投放恶意代码，Zoom 和 GitLab 被列为受影响站点。此事影响嵌入 Optimizely 脚本的网站及其访客，核心风险在于第三方 JavaScript 供应链：客户站点依赖外部脚本，供应商被入侵后恶意代码可随脚本进入多个站点。现有信息没有说明完整的受影响名单、植入持续时间或修复状态。

hackernews · kristjansson · 11月16日 23:00 · [社区讨论](https://news.ycombinator.com/item?id=50524767)

**「背景」** Optimizely 是提供 A/B 测试、个性化和实验功能的平台，客户通常在自己的页面中嵌入其 JavaScript 片段，因此该脚本会随页面加载并在多个站点上执行。BleepingComputer 将此次事件描述为针对 Optimizely 的供应链攻击，并称恶意 JavaScript 被加载到 Zoom、CNN、BBC、Salesforce 和 GitLab 等网站。

**「影响」** 对在页面中嵌入 Optimizely 脚本的站点来说，直接后果是：一旦该第三方脚本被篡改，站点即使不发布新代码也可能向访客下发恶意内容，因此受影响团队需要排查自身页面是否加载了异常脚本，并重新评估第三方脚本的加载与审批方式。Optimizely 的客户名单包括 Zoom 等 10,000 多家企业，这意味着排查范围可能超出最初被点名的站点；评论中提出的自行托管（vendoring）或限制脚本属于应对建议，并非已确认的修复措施。

**「社区讨论」** 评论把焦点放在第三方脚本治理上：stickfigure 认为 Google Tag Manager 让营销部门绕过工程团队添加标签，导致新闻页面加载约 10MB 的 JavaScript；mcoliver 主张 Optimizely 和大流量站点应设置发布冷却、分阶段上线和自动安全检查，并质疑为何缺乏问责。eax-eip 则提到，尚不清楚攻击者如何获得跨客户写入权限，并强调 Optimizely 的 CDN 只是分发其收到的内容，Optimizely 自家站点也受到影响。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.m.wikipedia.org/wiki/Optimizely">Optimizely - Wikipedia</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/optimizely-supply-chain-attack-infects-major-brands-sites-with-malware/">Optimizely supply chain attack infects major brands&#x27; sites with...</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/ad-tech-firm-optimizely-confirms-data-breach-after-vishing-attack/">Ad tech firm Optimizely confirms data breach after vishing attack</a></li>

</ul>
</details>

**标签**: `#supply-chain-security`, `#third-party-scripts`, `#web-security`, `#malware`, `#javascript`

---

<a id="item-tech-news-8"></a>
### [Marimba：单次冻结 ASR 编码器复用多任务语音查询](https://www.reddit.com/r/MachineLearning/comments/1xxsqro/marimba_a_system_one_model_for_speech_r/) ⭐️ 7.0/10

Reddit 研究帖发布了 Marimba 的论文、代码和 Apache-2.0 权重：对每个 8 秒音频窗口只跑一次冻结的 Qwen3-ASR-0.6B 编码器，再用文本问题查询词项、语言、话轮结束、说话人变化和人数，并返回校准概率。作者称，在 1,000 道公开问题的 9 项测试中有 6 项匹配或超过 Qwen3-Omni（30B-A3B），但在 Speech Commands 上落后；词项检测是零样本解码器假设打分加 Platt 校准，语言 ID 在 300 段 FLEURS 上为 100%。作者报告说话人变化在 AMI/VoxConverse 上 AUROC 为 0.966–0.980，高于 ECAPA，说话人计数优于 pyannote 3.1。局限也被明确列出：话轮结束读数在 Smart Turn 数据上训练，仅在该分布内有效；在 Smart Turn 自身测试集上 AUROC 为 0.930，低于 Smart Turn v3.2 的 0.982，且在 CochlScene 场景分类上所有头仅达随机水平。

reddit · r/MachineLearning · /u/solanotodesch · 11月16日 15:47

**「背景」** 这是作者继上周帖子之后的后续发布，本次补齐了论文、代码、Apache-2.0 权重与 pip 包。其技术前提是把一个冻结的 Qwen3-ASR-0.6B 编码器当作共享特征提取器：每个 8 秒音频窗口只做一次前向，再由挂在冻结层上的小型读出层回答“是/否、选项、分数”三类查询——话轮结束用第 18 层读出，说话人变化与计数用第 12 层读出；词项检测则不做训练，直接对 ASR 解码器的贪心与 4 条 beam 假设打分并做 Platt 校准，语言识别复用 ASR 模型自带的语言分数。

**「影响」** 对想在低成本或本地环境复用 ASR 编码器的开发者，Marimba 提供了可直接安装的 \`marimba-audio\` 包和 Apache-2.0 权重；但这些结果只在所列基准上成立，部署到新任务前应按目标域重新验证，CochlScene 上的随机水平说明不能假定零样本迁移。

**标签**: `#speech-recognition`, `#model-efficiency`, `#confidence-calibration`, `#audio-benchmarks`, `#asr`

---

<a id="item-tech-news-9"></a>
### [Duetto 不微调，用采样时 logit 引导实时爵士伴奏](https://www.reddit.com/r/MachineLearning/comments/1xxkyh3/steering_a_pretrained_music_transformer_at/) ⭐️ 7.0/10

Duetto 是作者自述的实时爵士 MIDI 伴奏项目：它直接使用预训练的 Anticipatory Music Transformer（Thickstun 等，2023），不进行微调，而是在每次采样前由规则层修改 logits——屏蔽不允许的音符（如必须等待的手、超出音域的音、非拍上的低音），并对当前和弦音、强拍导音或待引用乐句的下一音加偏置。系统把演奏者与模型的音符放在同一事件序列中逐音续写，可扮演独奏、伴奏和走动低音，并提前采样约 1 秒音乐；演奏者输入后重采样尚未播放的部分以降低延迟。作者报告在 3080 Ti 上中模型约 12 ms/音符、大模型约 18 ms/音符，大模型在 Jetson Orin Nano 上约 90 ms/音符；演示中约 61% 的独奏音符来自引用乐句或主题。作者也说明它仍会偏离演奏者、反应难以预测，模型创意与规则偏置之间的平衡很脆弱；代码可免费用于非商业用途。

reddit · r/MachineLearning · /u/GGAllin43 · 11月16日 09:19

**「背景」** Duetto 构建在 Thickstun 等人于 2023 年提出的 Anticipatory Music Transformer 之上：该模型将事件序列与控制序列交错排列，支持“预见式”生成与音乐补全（infilling），因此适合与演奏者逐音交替续写（tool-1-1、tool-1-3）。通常要让预训练音乐模型服从特定乐器、音域或和声约束，需要针对目标风格做微调；Duetto 则保留原模型权重不变，在每次采样前用规则层改写 logits，把控制成本从训练阶段转移到推理阶段。

**「影响」** 对实现者来说，实时性不只取决于单音采样速度；系统还要维护约 1 秒的预采样缓冲，并在每次演奏输入后重新采样未播放部分，因此 MIDI 调度和状态管理是集成时必须处理的部分。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://arxiv.org/abs/2306.08620">[2306.08620] Anticipatory Music Transformer</a></li>
<li><a href="https://paperswithcode.co/paper/2306.08620">Anticipatory Music Transformer (arXiv...) | Papers with Code</a></li>

</ul>
</details>

**标签**: `#music generation`, `#sampling-time control`, `#transformers`, `#MIDI`, `#real-time AI`

---

<a id="item-tech-news-10"></a>
### [美与九国签署《旧金山宣言》共保超级智能供应链](https://www.state.gov/releases/office-of-the-spokesman/2026/11/the-san-francisco-declaration-on-the-secure-foundations-of-enduring-prosperity/) ⭐️ 7.0/10

2026 年 11 月 15 日，美国与澳大利亚、印度、以色列、日本、韩国、卡塔尔、新加坡、阿联酋和英国签署《旧金山宣言》，确认经济安全是国家安全的基础，并同意共同保护支撑超级智能（SI）供应链的敏感技术和关键基础设施。宣言提出设立五个工作组，分别负责创新政策框架、SI 在关键领域的应用、SI 全栈供应链协作、安全港与供应链安全枢纽，以及 SI 的安全与韧性。该文件目前属于政策宣言，未公布各工作组的具体承诺、时间表或约束性措施。

telegram · zaihuapd · 11月16日 10:40

**「背景」** 该宣言在 Pax Silica Founders Retreat 上宣布，由美国负责经济事务的副国务卿 Jacob Helberg 主持。公开资料显示，其目标包括降低伙伴国在关键矿产、AI 模型和半导体芯片上对美国对手的依赖，这为五个工作组所涉及的供应链协作提供了背景。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/San_Francisco_Declaration_on_the_Secure_Foundations_of_Enduring_Prosperity">San Francisco Declaration on the Secure Foundations of Enduring Prosperity</a></li>

</ul>
</details>

**标签**: `#AI policy`, `#AI supply chain`, `#international cooperation`, `#semiconductor supply chain`, `#superintelligence`

---

<a id="item-tech-news-11"></a>
### [阿里等中国 AI 公司据报收紧新模型网络攻击能力](https://www.bloomberg.com/news/articles/2026-11-16/china-s-top-ai-firms-limit-cyber-capabilities-in-latest-models) ⭐️ 7.0/10

据该条目转述的 Bloomberg 报道，阿里巴巴、腾讯和月之暗面等中国头部 AI 公司在新一代模型中削弱了进攻性网络能力，同时提升防御表现。报道称，阿里最新旗舰 Qwen 未开放权重，用户无法下载并自定义完整版本；腾讯在本月发布 Hy4 前已削减网络功能。报道还将这些调整与商务部上月公布的出口管制草案联系起来：该草案拟禁止可攻击关键基础设施或政府网络的 AI 工具出口。上述限制的具体技术细节、适用范围和生效条件尚未披露。

telegram · zaihuapd · 11月17日 02:20

**「背景」** 据源报道，中国商务部上月公布了一份出口管制草案，拟禁止出口可用于攻击关键基础设施和政府网络的 AI 工具，这为厂商在新模型中主动削弱进攻性网络能力提供了政策背景。腾讯在本月发布 Hy4 之前就已削减相关网络功能，说明这一调整在草案公布后已开始落实到具体产品。另一条需要理解的背景是开放权重：Qwen 系列此前允许用户下载并自行定制完整模型，而阿里这次最新旗舰未开放权重，使外部开发者无法再获得可自行微调的完整版本。

**「影响」** 对开发者而言，直接影响是阿里最新旗舰 Qwen 不再提供可下载的完整权重，用户无法自行微调或在本地部署完整版本，只能使用厂商提供的版本；腾讯在发布 Hy4 前已削减网络功能，依赖该类模型做安全测试或红队评估的团队需要重新验证原有进攻性用例是否仍能执行。由于相关出口管制仍是上月公布的草案，这些收紧目前属于厂商主动限制，而非已生效的出口禁令。

**标签**: `#AI governance`, `#cybersecurity`, `#export controls`, `#open weights`, `#China AI`

---

<a id="item-tech-news-12"></a>
### [Xbox 确认 Project Helix 是可玩 PC 游戏的主机](https://www.ign.com/articles/xbox-confirms-project-helix-is-a-console-capable-of-playing-games-from-your-pc) ⭐️ 7.0/10

Xbox 已确认，下一代计划 Project Helix 被设计成一台能玩 PC 游戏的主机，而不是一台能玩主机游戏的 PC。Xbox 在 11 月 15 日上线的 25 周年纪念杂志中公布这一方向，下一代业务副总裁 Jason Ronald 称目标是“终极游戏机”，让玩家可直接访问四代 Xbox 游戏库与进度，消除主机与 PC 游戏之间的人为界限。官方尚未公布设备形态与发售时间，外界传闻最早 2027 年底。

telegram · zaihuapd · 11月17日 02:40

**「背景」** Project Helix 属于 Xbox 已公开的下一代主机计划；Xbox 主机过去主要运行专门的主机版游戏，PC 游戏库通常不在同一台设备上直接可用。Xbox 将 Helix 描述为能直接访问四代 Xbox 游戏库与进度的“终极游戏机”，显示其想用同一台设备连接原本分隔的主机与 PC 游戏生态。

**「影响」** 对现有 Xbox 用户而言，官方称可直接访问四代 Xbox 游戏库与进度，这是目前最明确的兼容性承诺；但设备形态、价格和发售时间未公布，实际兼容范围与迁移方式仍待说明。

**标签**: `#Xbox`, `#Project Helix`, `#PC gaming`, `#gaming consoles`, `#hardware`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [英伟达 CEO 辞职、国会易主：ETF 专家谈 AI 交易可能如何变化](https://www.cnbc.com/2026/11/14/nvidia-ai-trade-data-centers-congress.html) ⭐️ 7.0/10

英伟达创始人兼 CEO 黄仁勋辞职后，Roundhill 与 Yorkville Ives 的嘉宾在 CNBC 节目“ETF Edge”中表示，大型科技股及其他 AI 芯片厂商可能从英伟达的动荡中受益。Yorkville Ives 合伙人 Dan Ives 估计，民主党在 11 月 3 日赢下国会控制权后，可能使已规划的数据中心减少 10%（低端）至 15%-20%（高端），但他称需求仍约为供给的四倍。

rss · CNBC Finance · 11月16日 12:13

**「背景」** 英伟达在经历动荡一周后宣布，创始人兼 CEO 黄仁勋辞职，首席财务官科莱特·克雷斯出任临时 CEO 并继续负责财务，直到确定正式继任者；此前民主党在 11 月 3 日选举中赢得国会控制权，市场因此关注数据中心建设可能面临的政策阻力。

**「谁可能受影响」** Roundhill Investments 首席执行官 Dave Mazza 在 CNBC“ETF Edge”节目中判断，如果投资者因英伟达动荡而转向其他芯片来源，那些已拥有现成算力的大型超大规模云厂商反而可能受益，因为算力会变得更有价值。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.bbc.com/news/live/c6zjry11v8w1t">Huang agrees to appear before Congress, US lawmakers... - BBC News</a></li>
<li><a href="https://finance.yahoo.com/technology/ai/articles/nvidia-ceo-jensen-huang-resigns-110116748.html">Nvidia CEO Jensen Huang Resigns — CFO Collette Kress in as...</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#AI trade`, `#ETFs`, `#semiconductors`, `#policy risk`

---

<a id="item-finance-news-2"></a>
### [卢特尼克因英伟达相关关系受质疑，其子执掌的坎托减持英伟达](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 7.0/10

CNBC 报道，美国商务部长霍华德·卢特尼克因其子执掌的坎托·菲茨杰拉德与英伟达的持股及业务关系面临利益冲突和国家安全质疑。据 CNBC 对证券申报文件的分析（不含期权），该公司报告的英伟达持股在 2025 年 9 月至 2026 年 3 月间减少 49%，从约 350 万股降至 178 万股。

rss · CNBC Finance · 11月16日 12:14

**「背景」** 卢特尼克于 2025 年 2 月离开坎托出任商务部长，该公司现由其子布兰登和凯尔领导；商务部负责出口管制，包括实体清单。Axios 报道称，他曾多次抵制对涉嫌经新加坡向中国转运英伟达 AI 芯片的 Megaspeed 采取行动，并收到过有关英伟达 CEO 黄仁勋与一名疑似中国间谍关系的机密情报警告；报道称无证据表明其子提前知情或持股变动与警告有关，坎托称 13F 文件反映的持仓是为客户互换交易而进行。

**标签**: `#Nvidia`, `#Howard Lutnick`, `#Cantor Fitzgerald`, `#China export controls`, `#conflict of interest`

---

<a id="item-finance-news-3"></a>
### [英特尔及 CEO 陈立武遭股东集体诉讼](https://www.investing.com/news/stock-market-news/intel-sued-by-shareholders-following-29-stock-plunge-5028171) ⭐️ 7.0/10

英特尔及其 CEO 陈立武、CFO 津斯纳被股东提起集体诉讼，诉讼称公司在 2026 年 10 月 29 日发布不及预期的第四季度营收和利润预测前，隐瞒了 PC 需求疲软和库存积压的影响。预测发布次日股价暴跌 28.6%，市值蒸发约 1400 亿美元；这起由密歇根州一家养老基金牵头、在圣何塞联邦法院提起的诉讼，索赔对象为 2026 年 7 月 23 日至 10 月 29 日买入股票的投资者。

telegram · zaihuapd · 11月16日 11:10

**「背景」** 此前，英特尔正通过售股筹集 230 亿美元来扩张代工业务，但个人电脑销售走弱和库存积压已拖累其客户端业务。公司 CFO 还表示，今年预计无法实现正现金流，PC 市场低迷可能至少持续到明年上半年。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://wccftech.com/intel-ceo-lip-bu-tan-named-defendant-class-action-lawsuit-pc-sales-slowdown/">Intel CEO Lip - Bu Tan Named As Defendant In New Class - Action ...</a></li>
<li><a href="https://www.haiai123.com/en/hot/5387">Intel shares plunge about 28 . 6 % after weak guidance - HaiAi123</a></li>

</ul>
</details>

**标签**: `#Intel`, `#shareholder class action`, `#earnings guidance`, `#stock plunge`, `#semiconductors`

---