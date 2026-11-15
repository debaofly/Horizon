---
layout: default
title: "Horizon Summary: 2026-11-15 (ZH)"
date: 2026-11-15
lang: zh
---

> 从 39 条内容中筛选出 7 条重要资讯。

---

**科技新闻**
1. [Lovable 应用因 RLS 不足泄露护照与逾 20 万条私信](#item-tech-news-1) ⭐️ 8.0/10
2. [EFF：科技公司再次改写隐私概念](#item-tech-news-2) ⭐️ 7.0/10
3. [Project Zero 漏洞披露期限改为 90 天](#item-tech-news-3) ⭐️ 7.0/10
4. [Show HN：约 200 行纯 JAX 复现 DeepSeek V3](#item-tech-news-4) ⭐️ 7.0/10
5. [星舰第 15 次试飞入轨部署星链 V3，助推器返场中止](#item-tech-news-5) ⭐️ 7.0/10
6. [Cloudflare 以 Apache 2.0 开源 AI 代理浏览器 Kitesurf](#item-tech-news-6) ⭐️ 7.0/10
7. [意大利以违规读取相册罚 Meta 8.05 亿欧元](#item-tech-news-7) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Lovable 应用因 RLS 不足泄露护照与逾 20 万条私信](https://www.crissyfield.de/research/lovable-en/) ⭐️ 8.0/10

安全研究团队 Crissy Field 报告称，部分用 Lovable 构建的应用因 Supabase 行级安全（RLS）配置不足，暴露了护照信息和超过 20 万条私人消息。Lovable 安全负责人 Igor Andri 在讨论中回应称，根因正是其发布前自动扫描和可选的深度 SAST 扫描要捕获的 RLS 问题；两项扫描对所有用户免费，用户可让 Lovable 协助“修复”发现项，或开启后台自动修复。现有材料未说明受影响应用的具体数量，也未说明这些应用所属的组织或用户范围。

hackernews · armcat · 11月14日 17:43 · [社区讨论](https://news.ycombinator.com/item?id=50499017)

**「背景」** 这些事件涉及 Lovable 生成、后端使用 Supabase 的应用：Row-Level Security（RLS）是 PostgreSQL 的行级访问控制，表若未启用 RLS 或策略放行匿名请求，浏览器端公开的 anon key 就能经 Supabase Data API 访问数据。Supabase 曾因 public schema 默认向 anon、authenticated 等角色授权而受到批评，开发者要求能够关闭 anon key 对数据库的直接访问。自 2026 年 10 月 30 日起，Supabase 改为新表默认不向 anon、authenticated 和 service\_role 授权，必须显式 grant 后 Data API 才能访问，这也使既有项目与新项目的默认风险不同。

**「影响」** 受影响应用的用户面临护照信息和私信被未授权读取的风险；开发者需要在发布前逐表检查 Supabase RLS 策略，并进行未认证或越权访问测试，而不能把平台扫描当作唯一保障。

**「社区讨论」** 讨论的焦点不只是 Lovable：有评论者援引 Supabase 讨论称，Supabase 长期用较宽松的默认设置降低上手门槛，相关默认值据称已在 10 月 30 日修复，但既有项目可能仍沿用旧设置（该说法来自评论，未获独立确认）。也有评论者认为，AI 生成应用让这类越权访问更容易被发现和批量利用，而大量普通用户并不了解自己所用应用的风险。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.com/orgs/supabase/discussions/4547">Option to disable anon key access to database · supabase ...</a></li>
<li><a href="https://www.putthrough.com/blog/supabase-permission-denied-for-table">Supabase “permission denied for table” (42501): the safe fix</a></li>

</ul>
</details>

**标签**: `#security research`, `#row-level security`, `#Supabase`, `#AI app builders`, `#data exposure`

---

<a id="item-tech-news-2"></a>
### [EFF：科技公司再次改写隐私概念](https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again) ⭐️ 7.0/10

电子前沿基金会（EFF）发文审视科技公司再次试图重新定义隐私概念的做法，议题涉及 AI 会议记录工具、数据融合以及职场监控中的同意问题。现有材料仅提供文章主题与讨论方向，未呈现 EFF 的具体案例、政策主张或可操作建议，因此无法核实其完整论证。相关背景包括 AI 会议记事员和数据融合，但文章是否提出新的监管或产品要求尚不明确。

hackernews · gslin · 11月14日 12:45 · [社区讨论](https://news.ycombinator.com/item?id=50496602)

**「背景」** 电子前沿基金会（EFF）是一家以维护数字权利为目标的非营利组织，其 Deeplinks 博客长期发布针对科技公司隐私实践的评论（tool-1-3）。这篇分析延续该脉络，主张科技公司正再次试图重新界定“隐私”概念本身，而非仅仅改变某一项具体做法；其具体论点与所涉企业名称在现有材料中未有更多细节。

**「实际影响」** 对职场用户而言，这一转变的具体后果是退出成本被转嫁给个人：有评论者报告，如今连经理与同事的一对一会议也会被 AI 记录器录音并上传，而拒绝参与可能意味着难以继续受雇。组织在部署此类工具时，应让会议发起者在开始前明确记录范围和保存方式，并允许参会者无需说明理由即可关闭转录。

**「社区讨论」** 评论者 toddmorey 描述了专业会议普遍被 AI 记事员录音、员工难以退出而不影响就业的处境，并询问能否把“本次会议无需转录”变成规范。另一部分讨论则从无障碍角度提出，实时转录眼镜对聋人和重听者可能有价值，但本地处理仍可能因一个条件分支而变成数据留存，凸显同意与可访问性之间的张力。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.eff.org/">Electronic Frontier Foundation | Defending your rights in the ...</a></li>

</ul>
</details>

**标签**: `#privacy`, `#AI surveillance`, `#tech policy`, `#data protection`, `#workplace AI`

---

<a id="item-tech-news-3"></a>
### [Project Zero 漏洞披露期限改为 90 天](https://projectzero.google/2026/11/disclosure-policy.html) ⭐️ 7.0/10

Project Zero 将把漏洞披露期限定为向厂商报告后 90 天。评论中引述的公告还列出了分阶段安排：2027 年 2 月 2 日改为 60 天，2028 年 1 月 3 日改为 30 天；这些具体日期和后续缩短计划来自评论转述，提供的来源正文未予独立确认。

hackernews · hacb · 11月14日 11:13 · [社区讨论](https://news.ycombinator.com/item?id=50496051)

**「背景」** Project Zero 是 Google 的漏洞研究团队，其披露期限一直需要在给厂商留出修复时间与尽早提醒用户之间取得平衡。该团队过去的政策以 90 天披露窗口为基础，并在 2021 年因“90+30 天”宽限安排的变化受到安全社区关注。此次评论中引述的新规则则把披露窗口分阶段缩短到 60 天和 30 天。

**「影响」** 对软件厂商而言，90 天期限把从收到报告到公开披露的协调窗口明确限定为三个月；若后续缩短至 60 天或 30 天，修复和发版周期较长的项目将需要提前调整安全响应流程。评论中有人以 Ubuntu 为例担心大型发行版需要更长时间，这属于社区判断，而非已证实的结果。

**「社区讨论」** 评论区的分歧集中在固定期限能否兼顾施压与修复：有观点主张应立即公开，否则厂商没有足够动力修复；也有人认为 Ubuntu 等大型项目需要远超 90 天的时间。另有评论讨论漏洞发现方是否应向开源项目提供补丁访问，但这更多是推测性担忧。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://cje.io/2021/05/08/on-project-zeros-90-30-vulnerability-disclosure-policy-changes/">On Project Zero &#x27;s 90 + 30 vulnerability disclosure policy changes</a></li>

</ul>
</details>

**标签**: `#vulnerability disclosure`, `#cybersecurity`, `#Project Zero`, `#Google`, `#software security`

---

<a id="item-tech-news-4"></a>
### [Show HN：约 200 行纯 JAX 复现 DeepSeek V3](https://github.com/Vaibhaav-Tiwari/deepseek-v3-jax) ⭐️ 7.0/10

GitHub 上的 Show HN 项目 deepseek-v3-jax 用约 200 行纯 JAX 代码复现 DeepSeek V3，面向希望从第一性原理理解 LLM 实现和推理流程的开发者。从代码规模看，它更像精简的教学与实验性实现，而非可直接用于生产的推理栈。项目已公开；一名使用 RX 7600 XT 16GB 的评论者报告称其在 ROCm 上端到端跑通，但这属于个人运行经验，尚未经过独立验证。

hackernews · VaibhaavTiwari · 11月14日 15:04 · [社区讨论](https://news.ycombinator.com/item?id=50497589)

**「背景」** DeepSeek V3 是 DeepSeek 的大语言模型；这个 Show HN 项目由第三方开发者用 JAX 做极简复现，并非官方发布的新模型或推理栈。JAX 是谷歌生态中的数值计算与自动微分库，写法接近 NumPy，并能把计算编译到 GPU 等加速器，因此常被用于从第一性原理拆解 LLM 的教学项目。约 200 行的规模表明，它重在把核心推理路径写清楚，而不是覆盖生产部署所需的完整工程层。

**「影响」** 对想在本地研究 LLM 内部实现或尝试 AMD ROCm 的开发者，它提供了一个很小的参考起点；但本地运行可能仍需针对 GPU 做环境适配。上述 RX 7600 XT 16GB 用户称需设置 HSA\_OVERRIDE\_GFX\_VERSION=11.0.0，因为 JAX 插件会拒绝 gfx1102。

**「社区讨论」** 评论主要肯定从零重建模型的学习价值：有人称赞这种第一性原理做法，也有人询问从 Java/Python 背景进一步理解推理流程的路线图。讨论更多聚焦学习路径，而非性能基准。

**标签**: `#DeepSeek V3`, `#JAX`, `#LLM inference`, `#ROCm`, `#open-source code`

---

<a id="item-tech-news-5"></a>
### [星舰第 15 次试飞入轨部署星链 V3，助推器返场中止](https://www.spacex.com/launches/starship-flight-15) ⭐️ 7.0/10

SpaceX 于当地时间 11 月 13 日从得州发射星舰第 15 次试飞，飞船成功入轨并部署全部 26 颗 Starlink V3 卫星，其中 3 颗带摄像头用于检查隔热瓦。原计划由发射塔机械臂先后捕获助推器与飞船（即“塔捕”），但助推器因技术问题中止返场，改在墨西哥湾受控溅落并爆炸，具体原因未公布，两级同时回收因此未能实现。关于飞船，较早的报道称其将在轨约 22 小时、绕地球约 14 圈后于次日返回 Starbase 尝试首次轨道级飞船塔捕；另一则消息则称 SpaceX 宣布飞船在约 22.5 小时飞行后已被机械臂成功捕获，两种说法在时序上不一致，尚待官方进一步确认。

telegram · zaihuapd · 11月14日 03:03

**「背景」** “塔捕”是指返回的助推器或飞船不落地、不落海，而由发射塔机械臂夹住箭体上的承接点；在本次任务之前，星舰尚未实现助推器与飞船在同一任务中双双被塔臂捕获。SpaceX 未公布本次助推器中止返场的原因；CNN 的直播报道提到，V3 版超重型助推器此前存在发动机问题，曾出现部分发动机提前熄火。

**「影响」** 若飞船塔捕确实完成，将是轨道级飞船首次由发射塔机械臂直接承接回收，直接影响星舰的复用周转流程；而助推器返场中止表明超重型助推器的回收环节仍需在后续试飞中重新验证，两级同步回收的时间点相应推后。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.cnn.com/2026/11/13/science/live-news/spacex-starship-flight-15-ship-catch">Live updates: SpaceX Starship nails historic ship catch in... | CNN</a></li>

</ul>
</details>

**标签**: `#SpaceX`, `#Starship`, `#spaceflight`, `#reusable rockets`, `#Starlink`

---

<a id="item-tech-news-6"></a>
### [Cloudflare 以 Apache 2.0 开源 AI 代理浏览器 Kitesurf](https://www.phoronix.com/news/Cloudflare-Kitesurf-Open-Source) ⭐️ 7.0/10

Cloudflare 以 Apache 2.0 许可证开源了面向 AI 代理的无状态浏览器 Kitesurf，代码已发布在 GitHub。Kitesurf 基于 Cloudflare Workers 构建，无需浏览器容器即可解析 HTML、处理 CSS 并执行 JavaScript。Cloudflare 表示，它相比 Chromium 占用更少 CPU 和内存，并可在全球 Workers 网络上按需扩展；目前未提供基准测试或独立验证结果。

telegram · zaihuapd · 11月14日 09:33

**「背景：为什么代理浏览器要脱离容器」** AI 代理访问网页时通常依赖 Playwright、Puppeteer 等工具驱动容器中的无头 Chromium，这类方案需要完整的浏览器进程，CPU 与内存开销大，横向扩容也受容器调度限制。Kitesurf 的做法是把 HTML 解析、CSS 处理与 JavaScript 执行放进 Cloudflare Workers 的无状态运行环境，因此不再需要常驻浏览器容器。Cloudflare 对外的说法是它比 Chromium 占用更少 CPU 和内存，并可直接依托全球 Workers 网络按需扩展，但这一比较目前尚无公开基准数据支撑。

**「对开发者与代理部署的影响」** 对需要为 AI 代理批量抓取或执行网页的开发者而言，Kitesurf 提供了不必为每个会话启动 Chromium 容器的路径：它以 Apache 2.0 许可发布、可直接跑在全球 Workers 网络上按需扩缩，因此代理基础设施的部署与隔离方式可以改为无状态函数调用。但代价是它并非完整浏览器渲染环境，依赖完整 DOM、布局或复杂浏览器特性的页面行为可能与 Chromium 不一致，且 Cloudflare 所称的 CPU 与内存占用更低目前只是厂商说法、缺乏公开基准；在替换现有无头浏览器方案前，应先针对目标站点验证解析与脚本执行兼容性。

**标签**: `#Cloudflare`, `#AI agents`, `#browser`, `#open source`, `#Cloudflare Workers`

---

<a id="item-tech-news-7"></a>
### [意大利以违规读取相册罚 Meta 8.05 亿欧元](https://www.garanteprivacy.it/home/docweb/-/docweb-display/docweb/10321080) ⭐️ 7.0/10

意大利隐私监管机构 Garante Privacy 对 Meta 处以 8.05 亿欧元罚款，认定其 Facebook Android 应用在未取得具体同意的情况下读取了约 2000 万意大利用户的相册照片、视频和元数据。涉事功能是 2023 年上线的相册推荐，默认开启且授权提示笼统。监管机构责令 Meta 在 60 天内将默认设置改为关闭，并就相册访问单独征得用户同意；否则该功能不得向未有效授权的用户启用。

telegram · zaihuapd · 11月14日 14:37

**「背景」** 欧盟《通用数据保护条例》（GDPR）要求处理个人数据须基于具体、知情的同意，相册照片与视频属于其中的个人数据范畴。此次处罚针对的是 Facebook Android 应用于 2023 年上线的相册推荐功能，该功能默认开启，授权提示被认定为笼统，因此监管机构认定其未满足“具体同意”的要求。

**「整改要求」** 这意味着 Meta 需要在意大利调整 Facebook Android 的相册授权流程：默认关闭相册推荐，并把相册访问同意与一般授权分开；在完成前，该功能不能对未有效同意的用户启用。

**标签**: `#Meta`, `#隐私监管`, `#数据保护`, `#Android`, `#合规`

---