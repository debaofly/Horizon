---
layout: default
title: "Horizon Summary: 2026-11-13 (EN)"
date: 2026-11-13
lang: en
---

> From 48 items, 15 important content pieces were selected

---

**Technology News**
1. [Hacker News Discusses Anthropic IPO Terms and Valuation](#item-tech-news-1) ⭐️ 9.0/10
2. [Rust 1.100 stabilizes never type, custom allocators, and Cargo cooldowns](#item-tech-news-2) ⭐️ 8.0/10
3. [UMAP 0.6 ships recursive initialization and faster optimizers](#item-tech-news-3) ⭐️ 8.0/10
4. [smolmaxxing reports 16B LLM inference on sub-1GB iPad and TV box](#item-tech-news-4) ⭐️ 7.0/10
5. [Google releases Gemini 4 Hydrogen with coding focus and flat pricing](#item-tech-news-5) ⭐️ 7.0/10
6. [Apple&\#x27;s Foundation Models Framework for Native App AI](#item-tech-news-6) ⭐️ 7.0/10
7. [Microsoft 365 email outage leaves enterprises without mail for hours](#item-tech-news-7) ⭐️ 7.0/10
8. [Write-up chains 22-year-old PostgreSQL type confusion into claimed RCE \(CVE-2026-6460\)](#item-tech-news-8) ⭐️ 7.0/10
9. [Chips and Cheese Interviews AMD&\#x27;s Mike Clark on Zen 6](#item-tech-news-9) ⭐️ 7.0/10
10. [SemiAnalysis: Jensen Huang Out at Nvidia, Alleges GPU Smuggling](#item-tech-news-10) ⭐️ 7.0/10
11. [TRIBE v2 audit finds no retinotopy or tonotopy, but MT+ motion selectivity](#item-tech-news-11) ⭐️ 7.0/10
12. [Apple details Secure Exclaves audio/video isolation and hardware-checked recording indicators](#item-tech-news-12) ⭐️ 7.0/10
13. [Claude Code 2.1.323 adds experimental JavaScript Code Mode](#item-tech-news-13) ⭐️ 7.0/10

**Financial News**
1. [Nvidia&\#x27;s Jensen Huang resigns amid alleged spy scandal, agrees to testify](#item-finance-news-1) ⭐️ 8.0/10
2. [礼来口服减重药在华获批，成为中国首个口服 GLP-1 减重疗法](#item-finance-news-2) ⭐️ 8.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Hacker News Discusses Anthropic IPO Terms and Valuation](https://ipo.anthropic.com/us/) ⭐️ 9.0/10

A Hacker News item pointing to an Anthropic IPO page has focused discussion on comment-cited deal terms rather than independently verified filings. Commenters cite a $70–78 price range, an $85.3B gross deal including a $26B private placement, and an implied market capitalization of about $968B at the $74 midpoint. They also cite Q3 2026 revenue of $17.0B, a roughly $81B October run rate, $900.9B in compute commitments through 2045, and the Nasdaq ticker ANT. Those figures come from commenters citing linked documents; the supplied item included no primary source text, so the page’s status and the figures’ accuracy could not be verified.

hackernews · josephljohnston · Nov 12, 11:46 · [Discussion](https://news.ycombinator.com/item?id=50465829)

**「Background」** Anthropic, the maker of Claude, had already set terms for its planned Nasdaq listing under the ticker ANT before this Hacker News discussion: an updated filing put the IPO at $70–$78 per share for 825 million shares, CNBC and Zacks reported. Commenters in the thread cite additional figures such as an implied valuation near $968 billion, but the item provides no independent confirmation of those details.

**「Fixed compute obligations now dominate the investment case」** Anthropic&\#x27;s filing discloses roughly $895–900 billion in aggregate spending commitments under purchase agreements and leases, substantially tied to compute and infrastructure — obligations that far exceed the liabilities on its current balance sheet. For IPO investors, that means the offering is as much a bet on servicing long-dated fixed payments out of revenue growth as it is on model quality, so the comment-cited ~$81B run-rate and $17.0B Q3&\#x27;26 revenue figures are the numbers that determine whether the commitments are manageable.

**「Community Discussion」** Commenters are split on whether the IPO timing signals confidence or pressure: one argues that venture investors would have delayed an IPO if recursive self-improvement were close, while another worries that later private rounds could be underwater at the low end of the range. Others expect local models and easy switching among models to erode frontier-lab pricing power.

<details><summary>References</summary>
<ul>
<li><a href="https://www.zacks.com/featured-articles/761/anthropic-ipo">Anthropic IPO 2026 Guide: Price Predictions, Dates, and ...</a></li>
<li><a href="https://www.cnbc.com/2026/11/10/anthropic-sets-price-range-of-70-to-78-in-upcoming-ipo.html">Anthropic sets price range of $70 to $78 in upcoming IPO - CNBC</a></li>
<li><a href="https://finance.yahoo.com/technology/ai/articles/anthropics-spending-commitments-surge-nearly-150617047.html?fr=sycsrp_catchall">Anthropic&#x27;s spending commitments surge to nearly $900 billion</a></li>
<li><a href="https://news.bloombergtax.com/financial-accounting/anthropic-ipo-filing-reveals-nearly-900-billion-in-future-debt">Anthropic IPO Filing Reveals Nearly $900 Billion in Future Debt</a></li>

</ul>
</details>

**Tags**: `#Anthropic`, `#IPO`, `#AI industry`, `#LLM economics`, `#Hacker News`

---

<a id="item-tech-news-2"></a>
### [Rust 1.100 stabilizes never type, custom allocators, and Cargo cooldowns](https://blog.rust-lang.org/2026/11/12/Rust-1.100.0/) ⭐️ 8.0/10

Rust 1.100 has shipped for Rust developers, stabilizing the never type and custom allocators and adding Cargo dependency-management safeguards. Cargo can now enforce a minimum publish age, or dependency cooldown, ignoring versions published more recently than the configured threshold unless they are already in Cargo.lock, and it warns by default about unused dependencies. \`cargo install\` now uses the existing lockfile in the \`.crate\` tarball by default, making \`--locked\` a no-op for that command.

hackernews · mbStavola · Nov 12, 18:39 · [Discussion](https://news.ycombinator.com/item?id=50472038)

**「Why dependency cooldowns needed a Cargo change」** Cargo&\#x27;s resolver normally selects the newest version of each dependency that satisfies the version requirement, so a freshly published — possibly compromised or broken — release can enter a build within hours of appearing on crates.io. RFC 3923 proposed a minimum-age configuration so that users can require dependency versions to age before the resolver picks them; per byteiota, Rust 1.100 implements that as an opt-in Cargo setting, and the release notes describe resolution that is aware of a minimum publish age.

**「Impact」** Projects that set Cargo&\#x27;s new minimum publish age will avoid resolving to crates published more recently than the configured window unless those versions are already pinned in Cargo.lock, reducing exposure to freshly published broken or malicious releases. CI and install scripts that pass \`cargo install --locked\` can drop the flag because it no longer changes behavior.

**「Community discussion」** Commenters welcomed the never type, custom allocators, and Cargo cooldowns as long-awaited changes, and one praised the new default unused-dependency warning. Another noted that stabilized APIs such as \`bool::toggle\(\)\`, \`Box::map\(\)\`, and \`str::trim\_prefix\(\)\` were not mentioned in the blog post, suggesting the release contains more than its headline list.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.rust-lang.org/2026/11/12/Rust-1.100.0/">Announcing Rust 1 . 100 .0 | Rust Blog</a></li>
<li><a href="https://byteiota.com/rust-1100-cargo-cooldowns/">Rust 1 . 100 : Cargo Dependency Cooldowns Are Here... | byteiota</a></li>
<li><a href="https://rust-lang.github.io/rfcs/3923-cargo-min-publish-age.html">3923 - cargo -min-publish-age - The Rust RFC Book</a></li>

</ul>
</details>

**Tags**: `#Rust`, `#programming languages`, `#Cargo`, `#dependency management`, `#memory allocation`

---

<a id="item-tech-news-3"></a>
### [UMAP 0.6 ships recursive initialization and faster optimizers](https://www.reddit.com/r/MachineLearning/comments/1xudaah/umap_06_new_initialization_new_optimizers_and/) ⭐️ 8.0/10

The UMAP project released umap-learn 0.6, adding a recursive initialization scheme, new optimizers built around hard-negative mining, and a claimed roughly 4x faster nearest-neighbor search through better use of PyNNDescent. According to the release post, the new optimizers make a fixed-seed run reproducible while using every CPU core; on 3 million arXiv papers the full run finishes in under 5 minutes, while a seeded 0.5 run takes 52 minutes single-threaded. The announcement also claims better quality at million-scale, with finer cluster structure and better kNN recall in fewer epochs. The new initialization and optimizers are opt-in because they change the output, enabled with compatibility\_layout=False; the project says future versions will make them the default.

reddit · r/MachineLearning · /u/lmcinnes · Nov 12, 13:51

**「Background」** UMAP constructs a k-nearest-neighbor graph and then optimizes a low-dimensional embedding; earlier versions started that optimization from spectral embedding or PCA and were designed around a limited portion of the attraction-repulsion spectrum. The 0.6 release changes both pieces: a recursive initialization builds a coarse UMAP layout before refinement, and new optimizers use hard-negative mining to handle much higher repulsion strengths.

**「Impact on existing pipelines」** Because 0.6 is a transition release that keeps 0.5.x behavior by default, upgrading alone will not deliver the speed or fidelity gains; users must set \`compatibility\_layout=False\` to opt into the new initialization and optimizers, and can then pick among the new Adam- and momentum-based layout optimizers via the \`optimizer\` parameter, with the original retained for compatibility. That opt-in changes the output coordinates, so downstream steps such as tuned cluster thresholds, saved embeddings, or comparisons against earlier runs need to be re-checked rather than assumed unchanged.

<details><summary>References</summary>
<ul>
<li><a href="https://umap-learn.readthedocs.io/en/latest/release_notes.html">Release Notes — umap 0.6.0 documentation - Read the Docs</a></li>
<li><a href="https://umap-learn.readthedocs.io/en/latest/optimizers.html">Choosing a UMAP Layout Optimizer — umap 0.6.0 documentation</a></li>

</ul>
</details>

**Tags**: `#UMAP`, `#dimensionality reduction`, `#open source`, `#performance`, `#machine learning`

---

<a id="item-tech-news-4"></a>
### [smolmaxxing reports 16B LLM inference on sub-1GB iPad and TV box](https://github.com/hyperionaidev/smolmaxxing/) ⭐️ 7.0/10

An open-source project, smolmaxxing, reports running 16B-parameter language models on a first-generation iPad Air and a Xiaomi TV box, each with less than 1GB of usable memory, at what its author calls &quot;decent speeds&quot; given the hardware. The author, posting as mrashad74, says the developed kernels, results, and modified models are being released openly — the models on Hugging Face under hyperionaidev — so others can reproduce the work and push toward more constrained devices. These figures are the author&\#x27;s own claims posted alongside the GitHub project and have not been independently verified, and the effort is described as recently started and early-stage.

hackernews · mrashad74 · Nov 12, 15:23 · [Discussion](https://news.ycombinator.com/item?id=50468888)

**「Background」** The approach depends on mixture-of-experts models, which keep a large total parameter count but need only a fraction of the weights to process a given token, so memory use can be traded against storage speed. The project&\#x27;s own documentation states that the iPad Air \(1st gen\) and Xiaomi TV Box builds run 8B and 16B mixture-of-experts models in roughly 1 GB of RAM by holding only part of each model in memory and reading the rest from flash as needed. That shifts the binding constraint from raw RAM capacity to flash read bandwidth, which is why the effort ships custom kernels and modified model files rather than stock inference code.

**「Impact」** For developers exploring edge inference, the useful artifact is the released kernels and modified checkpoints rather than the headline model size: reproducing the result means matching the author&\#x27;s specific kernels and model variants on comparable hardware, and because no independent benchmarks are available, throughput and output-quality claims should be measured on the actual target device before being relied on.

**「Community Discussion」** Commenters largely treated inference on old hardware as now mostly a problem of compute effort rather than engineering novelty: Farmadupe2 argued a modern coding agent can produce an inference engine in a single prompt because the core is multiplication, leaving hardware sourcing and SSH access as the hard part, while ahrjay reported getting an LLM running on Dreamcast hardware through a Windows CE boot project. nico contrasted a Qwen 2.5 0.5B fine-tune from a year ago — which needed a beefy Raspberry Pi and lacked reasoning — with a locally trained 6.5M-parameter model that now handles multi-step tasks, and cjdell described mixed results running tiny models for agentic tool calling on older 2–11GB Maxwell and Pascal GPUs.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/hyperionaidev/smolmaxxing/">GitHub - hyperionaidev / smolmaxxing : maxxing the ability to run...</a></li>

</ul>
</details>

**Tags**: `#LLM inference`, `#edge AI`, `#model optimization`, `#constrained hardware`, `#open source`

---

<a id="item-tech-news-5"></a>
### [Google releases Gemini 4 Hydrogen with coding focus and flat pricing](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/) ⭐️ 7.0/10

Google released Gemini 4 Hydrogen, a new model aimed at fast execution for everyday coding and agent workflows, and said it is available to developers, enterprises, and general users. The company set a single price of $1.50 per million input tokens and $7.50 per million output tokens. Google claims Hydrogen is 2.5 times faster than Gemini 3.8 Flash, raises Terminal-Bench 4.1 from 18.2% to 57%, and exceeds Argon on the Artificial Analysis index in its default tier; the supplied material does not include independent benchmark results or further technical detail.

hackernews · dvaplima · Nov 12, 18:01 · [Discussion](https://news.ycombinator.com/item?id=50471431)

**「Background」** Google’s Gemini line has used tier names such as Flash and Flash Lite to signal speed and cost, and the new Gemini 4 release adds element names: Hydrogen is compared with an Argon model as well as with Gemini 3.8 Flash. Coverage of the launch places Hydrogen at 51 on the Artificial Analysis Intelligence Index at the default high-thinking level, just above Argon’s 50, while Google describes it as a fast, cost-efficient model for agentic workflows.

**「Impact」** Developers and teams using Gemini&\#x27;s default tier should confirm which model their applications now call: one commenter reports that 3.8 Flash was replaced by 4 Hydrogen in the product, so existing workflows and cost assumptions should be checked against the new $1.50/$7.50 per-million-token rate.

**「Community discussion」** Commenters focused on the element-based naming, with one saying that seeing &quot;4 Hydrogen&quot; replace 3.8 Flash in the interface was confusing and not useful for comparing related models. Another argued that although Hydrogen is more capable than 3.8 Flash, its $1.50/$7.50 pricing matches the non-discounted 3.8 Flash rate and is considerably higher than what users currently pay for 3.8 Flash or 3.5 Flash Lite, questioning whether Google is abandoning its fast-and-cheap tier.

<details><summary>References</summary>
<ul>
<li><a href="https://interestingengineering.com/ai-robotics/google-gemini-4-hydrogen-coding-benchmark">Google launches Gemini 4 Hydrogen for faster coding and agentic...</a></li>
<li><a href="https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/">Introducing Gemini 4 Hydrogen for Agentic Workflows</a></li>

</ul>
</details>

**Tags**: `#Gemini`, `#Google AI`, `#model release`, `#AI pricing`, `#model naming`

---

<a id="item-tech-news-6"></a>
### [Apple&\#x27;s Foundation Models Framework for Native App AI](https://developer.apple.com/foundation-models-framework/) ⭐️ 7.0/10

Apple&\#x27;s Foundation Models framework is presented as a native way for developers to bring foundation-model capabilities into apps on Apple platforms. The linked page is official developer documentation, not a release note, and the supplied material does not give a version number, ship date, or detailed API changes. It is aimed at iOS and Swift developers who want to evaluate Apple&\#x27;s native model tooling for app features.

hackernews · kermatt · Nov 12, 21:13 · [Discussion](https://news.ycombinator.com/item?id=50474361)

**「What the framework is」** Foundation Models is Apple&\#x27;s Swift API for models that specialize in language understanding, structured output and tool calling, running either on-device or on Apple&\#x27;s Private Cloud Compute servers. Apple&\#x27;s WWDC 2026 session on the framework describes the additions developers now work with: Private Cloud Compute access, integration of third-party and open-source models, and vision capabilities, with the server-side model offering a 32K context window against roughly 4K on-device.

**「Impact」** For developers, the native path is not a blanket free cloud option: commenters point to Apple&\#x27;s conditions for no-cloud-cost Private Cloud Compute access—Small Business Program enrollment, fewer than two million first-time App Store downloads, and availability where Apple Intelligence is available—so apps must plan around those eligibility limits.

**「Community Discussion」** Commenters focused on access and adjacent tooling: btond quoted eligibility terms for using Foundation Models on Private Cloud Compute at no cloud API cost, while cj00 argued Apple&\#x27;s CoreAI work—adapting open-weight models to run natively with Swift—is flying under the radar. albertgoeswoof also reported using local models capably on an M1 with 8GB.

<details><summary>References</summary>
<ul>
<li><a href="https://developer.apple.com/documentation/foundationmodels">Foundation Models | Apple Developer Documentation</a></li>
<li><a href="https://developer.apple.com/videos/play/wwdc2026/241/">What’s new in the Foundation Models framework ... - Apple Developer</a></li>
<li><a href="https://blakecrosley.com/blog/foundation-models-image-input-ios-27">Foundation Models Image Input in iOS 27</a></li>

</ul>
</details>

**Tags**: `#Apple`, `#foundation models`, `#on-device AI`, `#Swift`, `#developer tools`

---

<a id="item-tech-news-7"></a>
### [Microsoft 365 email outage leaves enterprises without mail for hours](https://status.cloud.microsoft/) ⭐️ 7.0/10

Microsoft 365 email was unavailable for hours for enterprise users, with sysadmins reporting that service was still down into an eighth hour for an organization of more than 15,000 employees. Microsoft&\#x27;s status updates said it had validated an alternative health check on a subset of affected infrastructure, returned those servers to service, and was applying the change more broadly while preparing an automated process to detect and restart unresponsive servers. The updates did not identify a root cause, and user reports said Teams and Azure were working while email was not.

hackernews · dkpk · Nov 12, 18:20 · [Discussion](https://news.ycombinator.com/item?id=50471731)

**「Background」** Microsoft 365 email is delivered through Exchange Online, and Microsoft&\#x27;s recovery process relies on automated health checks that determine whether a server can safely return to service. In this incident, SecurityWeek reported that failed server health checks disrupted Outlook and other Microsoft 365 services, with no evidence of a cyberattack.

**「Impact」** For affected IT teams, email was cut off while Teams and Azure stayed available, so broad cloud-health checks could show green during an email outage. One sysadmin reported subscribing to Microsoft&\#x27;s RSS feed because the status page was not working well, a workaround other teams may need during recovery.

**「Community discussion」** Commenters mixed speculation with operational reports: one blamed Microsoft&\#x27;s AI-focused investment for declining reliability across GitHub and Azure, while sysadmins described email down for eight hours, Teams and Azure apparently unaffected, and the status page unreliable enough that an RSS feed became the usable update channel. Another called it the worst Microsoft 365 outage their organization had seen since adopting the service in 2019.

<details><summary>References</summary>
<ul>
<li><a href="https://www.securityweek.com/microsoft-365-outage-disrupts-outlook-exchange-online-and-teams/">Microsoft 365 Outage Disrupts Outlook, Exchange Online and ...</a></li>

</ul>
</details>

**Tags**: `#Microsoft 365`, `#cloud outage`, `#service reliability`, `#enterprise IT`

---

<a id="item-tech-news-8"></a>
### [Write-up chains 22-year-old PostgreSQL type confusion into claimed RCE \(CVE-2026-6460\)](https://mehmetince.net/part-3-6-how-i-ended-up-turning-a-22-year-old-postgresql-type-confusion-primitive-into-rce-cve-2026-6460/) ⭐️ 7.0/10

A newly published technical write-up describes turning a 22-year-old PostgreSQL type-confusion primitive into what the author labels remote code execution, under CVE-2026-6460. The available item does not name affected PostgreSQL versions, a patch, or independent reproduction, so the exploit chain is presented as the researcher’s account rather than a confirmed exposure. Commenters dispute the RCE label, arguing that because the chain begins with an authenticated database session it is better characterized as privilege escalation.

hackernews · ozirus · Nov 12, 18:22 · [Discussion](https://news.ycombinator.com/item?id=50471761)

**「The flaw behind the exploit」** CVE-2026-6460 is a type-confusion vulnerability in PostgreSQL caused by inadequate tracking of typed values. PostgreSQL&\#x27;s advisory states that an object creator can execute arbitrary code as the operating-system user running the database, primarily through \`ALTER TABLE ... SET DATA TYPE\`, with other DDL sequences such as \`ALTER TABLE ... ADD COLUMN; ROLLBACK; ALTER TABLE ... ADD COLUMN\` also serving as attack routes. Red Hat describes the trigger as an authenticated user with permission to create or alter database objects issuing specific data-definition commands, while a third-party tracker rates the issue CVSS 8.8 and lists no public proof-of-concept.

**「Impact」** If the commenters’ authenticated-session reading is correct, the operational consequence is scoped to environments where an attacker can already reach a database account: multi-tenant PostgreSQL operators should review role separation and cross-tenant access, and should not triage the issue as an unauthenticated network RCE without checking the write-up’s preconditions.

**「Community Discussion」** Several commenters, including logophobia and jmuguy, argue the exploit is better classified as privilege escalation because it requires an authenticated SQL session; logophobia says that makes it chiefly a multi-tenant database concern. Others praise the write-up for documenting the path and PostgreSQL internals, with amluto calling the underlying Datum/type-id design a code smell.

<details><summary>References</summary>
<ul>
<li><a href="https://www.postgresql.org/support/security/CVE-2026-6460/">PostgreSQL: CVE-2026-6460: PostgreSQL type confusion after ...</a></li>
<li><a href="https://access.redhat.com/security/cve/cve-2026-6460">CVE-2026-6460 - Red Hat Customer Portal</a></li>
<li><a href="https://www.thehackerwire.com/vulnerability/CVE-2026-6460/">CVE-2026-6460: PostgreSQL Remote Code Execution (RCE ...</a></li>

</ul>
</details>

**Tags**: `#PostgreSQL`, `#vulnerability research`, `#type confusion`, `#CVE`, `#exploit development`

---

<a id="item-tech-news-9"></a>
### [Chips and Cheese Interviews AMD&\#x27;s Mike Clark on Zen 6](https://chipsandcheese.com/p/talking-zen-6-with-mike-clark-at) ⭐️ 7.0/10

Chips and Cheese published an in-depth interview with AMD&\#x27;s Mike Clark about the Zen 6 CPU architecture. The available item summary does not include specific Zen 6 specifications, launch timing, performance claims, or product availability, so it is best treated as a design discussion rather than a product announcement.

hackernews · dverlaeckt80 · Nov 12, 14:12 · [Discussion](https://news.ycombinator.com/item?id=50467460)

**「Background」** Zen 6 succeeds AMD&\#x27;s Zen 5, and the interview focuses on how the architecture evolves from Zen 5 and how the standard Zen 6 core differs from the denser Zen 6c variant. Mike Clark, the original architect of Zen and AMD&\#x27;s chief architect for Zen 6, framed the family around five objectives: another major core performance increase, fuller use of the dense design style, better AI capability for agentic workloads, a lower-latency operating point, and expanded confidential computing. The dense Zen 6c variant is also described as gaining the full L3 cache.

**「Impact」** For hardware and software developers tracking AMD&\#x27;s future CPUs, the interview offers direct design context from an AMD architect, but the supplied material provides no compatibility, performance, or availability details to act on.

**「Community Discussion」** Commenter koutakun called the article interesting and said it is very rare to see CPU designers discuss their work at such depth.

<details><summary>References</summary>
<ul>
<li><a href="https://chipsandcheese.com/p/talking-zen-6-with-mike-clark-at">Talking Zen 6 with Mike Clark at AMD In-Depth</a></li>
<li><a href="https://daily.dev/posts/talking-zen-6-with-mike-clark-at-amd-in-depth-olc4f6a0w">Talking Zen 6 with Mike Clark at AMD In-Depth - daily.dev</a></li>
<li><a href="https://www.techpowerup.com/review/amd-zen-6-technical-deep-dive/4.html">AMD Zen 6 Technical Deep Dive - Zen 6 Core Architecture ...</a></li>

</ul>
</details>

**Tags**: `#AMD Zen 6`, `#CPU architecture`, `#hardware`, `#semiconductors`, `#technical interview`

---

<a id="item-tech-news-10"></a>
### [SemiAnalysis: Jensen Huang Out at Nvidia, Alleges GPU Smuggling](https://newsletter.semianalysis.com/p/nvidia-and-the-world-without-jensen) ⭐️ 7.0/10

SemiAnalysis reports that Jensen Huang is no longer Nvidia&\#x27;s CEO and that Colette Kress is interim CEO, while arguing—without substantiation in the excerpt—that his exit is tied to a board conduct investigation and alleged smuggling of restricted GPUs into China. The newsletter says its accelerator-tracking data shows more than 1.5GW of restricted Nvidia chips ultimately reached China, excluding Nvidia&\#x27;s China-specific chips designed to circumvent US rules, but the link to Huang&\#x27;s departure is presented as the authors&\#x27; belief. It adds that Nvidia is searching for a permanent CEO and names Ian Buck and Jonah Alben as internal technical candidates.

rss · Semianalysis · Nov 12, 18:06

**「Background」** On Nov. 8, 2026, Nvidia&\#x27;s board opened an investigation after Jensen Huang admitted to an extramarital affair and to concerns that he was the &quot;target of a foreign intelligence effort&quot; by China, according to CNN. Four days later, Nvidia announced his resignation as president, CEO, and board member, naming CFO Colette Kress as interim CEO and Harvey C. Jones as the board&\#x27;s first chair.

**「Export controls set to tighten」** SemiAnalysis expects the departure of Nvidia&\#x27;s most prominent internal opponent of tighter China rules to accelerate restrictions, pointing to the Remote Access Security Act, which the House passed and which would extend the Bureau of Industry and Security&\#x27;s authority to cover AI chips accessed remotely through cloud services rather than only chips shipped physically. If enacted, that would reach Chinese labs renting US cloud compute — a gap the current export-control regime does not clearly cover — while Nvidia and other US suppliers also lose the executive the newsletter credits with shaping the rules in their favor.

<details><summary>References</summary>
<ul>
<li><a href="https://www.cnn.com/2026/11/08/business/nvidia-investigation-ceo-jensen-huang">Nvidia CEO Jensen Huang admits affair as company launches ...</a></li>
<li><a href="https://investor.nvidia.com/news/press-release-details/2026/NVIDIA-Announces-CEO-Transition/default.aspx">NVIDIA Corporation - NVIDIA Announces CEO Transition</a></li>
<li><a href="https://chinaselectcommittee.house.gov/media/press-releases/house-passes-bipartisan-legislation-to-limit-adversaries-remote-access-to-critical-technology">House Passes Bipartisan Legislation to Limit Adversaries ...</a></li>
<li><a href="https://www.iaps.ai/research/remote-access-security-act">Remote Access Security Act (RASA) — Institute for AI Policy ...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#GPU export controls`, `#AI hardware`, `#semiconductor industry`, `#leadership change`

---

<a id="item-tech-news-11"></a>
### [TRIBE v2 audit finds no retinotopy or tonotopy, but MT+ motion selectivity](https://www.reddit.com/r/MachineLearning/comments/1xuillf/does_metas_brainresponse_model_tribe_v2_actually/) ⭐️ 7.0/10

In a solo, self-funded, non-peer-reviewed Reddit analysis, an independent researcher tested whether Meta&\#x27;s TRIBE v2—a model that predicts fMRI responses from video, audio, and text—recovers classic topographic brain maps. The audit notes that TRIBE v2&\#x27;s own paper did not test these maps and that its methods spatially average video features before prediction. Running checkerboard wedges and rings, hemifield flicker, moving dots, and tone sweeps through the model, with validation against a synthetic ground-truth control, the author reports no retinotopic map \(d=0.05, n.s.\) and no tonotopic map \(rho=-0.07, n.s., even with loudness controlled\). Motion selectivity was strong and localized to MT+ \(d=4.31, 52x enrichment over chance\), while eccentricity results became significant and &quot;correct&quot; under three separate stimulus-geometry controls, which the author interprets as an image-statistics confound rather than a genuine positional code.

reddit · r/MachineLearning · /u/Own\_Tank1283 · Nov 12, 17:16

**「What TRIBE v2 is, and the maps it was never tested on」** Meta FAIR released TRIBE v2, an open-weights tri-modal foundation model that predicts fMRI activity from video, audio, and text, trained on hundreds of hours of scans from hundreds of participants \(tool-2-2\). Retinotopy and tonotopy are the classic topographic maps probed with checkerboard wedges/rings, hemifield flicker, and tone sweeps, fitting voxel-wise response fields to test whether a model encodes position or frequency rather than just stimulus category — the standard check the source says TRIBE v2&\#x27;s paper omitted.

**「Impact」** Researchers using TRIBE v2 should not treat its outputs as a substitute for retinotopic or tonotopic mapping, and should include synthetic ground-truth and stimulus-geometry controls before interpreting apparent positional codes.

<details><summary>References</summary>
<ul>
<li><a href="https://smartchunks.com/meta-tribe-v2-brain-prediction-fmri-model/">Meta ’s New AI Predicts Brain Activity, And They Just... | Smart Chunks</a></li>

</ul>
</details>

**Tags**: `#neuroimaging`, `#fMRI`, `#model-evaluation`, `#computational-neuroscience`, `#reproducibility`

---

<a id="item-tech-news-12"></a>
### [Apple details Secure Exclaves audio/video isolation and hardware-checked recording indicators](https://security.apple.com/blog/secure-exclaves/) ⭐️ 7.0/10

Apple published a Nov. 12 post describing Secure Exclaves, an architecture that processes audio and video in a separate secure environment; in its ambient-awareness mode, the main system and apps receive only the necessary recognition results rather than raw data, according to the company. Apple says the technology is used in HomeView face and sound recognition and in the iPhone 18 Pro privacy indicator. On the iPhone 18 Pro, Apple says dedicated hardware verifies the microphone indicator dot&\#x27;s color, brightness and visibility before audio is allowed into the main system, and that Siri audio sessions must continuously show the dot for at least three seconds to prevent it from being covered or imitated. These are Apple&\#x27;s claims as summarized in the supplied post, not independently verified results.

telegram · zaihuapd · Nov 12, 09:13

**「Background」** Apple&\#x27;s Secure Exclaves are protected, compartmentalized runtimes that process camera and microphone data separately from the rest of the system. Apple says isolation features across many core silicon components keep these runtimes segregated, and that data processed inside a Secure Exclave cannot be accessed by the main system. This architecture is the basis for isolating HomeView&\#x27;s ambient camera and microphone sensing and for requiring a visible privacy indicator before full audio or video is released to the system.

**「Impact」** Under the described model, developers building ambient audio or video features would work from derived recognition results rather than raw feeds, and Siri audio sessions on the iPhone 18 Pro would need to satisfy the indicator-display conditions Apple describes; the supplied summary does not detail the APIs, exceptions, or how existing apps would be affected.

<details><summary>References</summary>
<ul>
<li><a href="https://security.apple.com/blog/secure-exclaves">Secure Exclaves and Ambient Sensing - Apple Security Research</a></li>
<li><a href="https://cyberinsider.com/apple-secure-exclaves-homeview-iphone-privacy-security/">Apple isolates HomeView camera and mic data with Secure ...</a></li>

</ul>
</details>

**Tags**: `#Apple`, `#security architecture`, `#privacy`, `#audio-video`, `#secure enclaves`

---

<a id="item-tech-news-13"></a>
### [Claude Code 2.1.323 adds experimental JavaScript Code Mode](https://code.claude.com/docs/en/changelog) ⭐️ 7.0/10

Claude Code 2.1.323, released November 12, introduces an experimental &quot;Code Mode&quot; that lets Claude invoke tools through JavaScript, and the feature can be turned off at the organization level. The same version tightens plugin management: plugins whose declared version range does not match will no longer be installed or updated, and \`plugin validate\` now performs type checking on TypeScript hooks. The changelog also lists .docx document upload support and a 30-second hook heartbeat among other improvements. The Code Mode capability is labeled experimental, and the details come from the vendor&\#x27;s own changelog rather than independent testing.

telegram · zaihuapd · Nov 13, 03:47

**「What Code Mode changes」** Claude Code is Anthropic&\#x27;s agentic coding tool, and until now it has driven its tools — reading files, running commands, editing code — through discrete, one-at-a-time tool calls issued by the model. Code Mode swaps that layer for a short JavaScript program that invokes the tools itself, which is also why the changelog treats it as an opt-out capability that an organization can disable rather than a default behavior. The plugin changes build on Claude Code&\#x27;s existing third-party plugin system, in which extensions declare supported version ranges and ship hooks that \`plugin validate\` can now type-check when written in TypeScript.

**「Plugin authors face blocked installs」** Plugin maintainers whose declared version ranges do not match the actual plugin version will find installs and updates refused, so ranges should be checked before publishing; per the docs, the range in an entry is compared against that plugin&\#x27;s version, and a plugin that states no version passes the check. Running \`plugin validate\` before release now also type-checks TypeScript hooks, catching hook-typing errors earlier.

<details><summary>References</summary>
<ul>
<li><a href="https://code.claude.com/docs/en/plugins/dependencies">Plugin dependencies - Claude Code Docs</a></li>

</ul>
</details>

**Tags**: `#Claude Code`, `#AI coding agents`, `#developer tools`, `#plugin management`, `#experimental features`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Nvidia&\#x27;s Jensen Huang resigns amid alleged spy scandal, agrees to testify](https://www.cnbc.com/2026/11/13/jensen-huang-nvidia-us-china-relations.html) ⭐️ 8.0/10

Former Nvidia CEO Jensen Huang resigned on Thursday and agreed to testify before Congress before Nov. 26 over his affair with a woman U.S. officials reportedly suspect was recruited by China&\#x27;s Ministry of State Security to gather information on him — an allegation China&\#x27;s Foreign Ministry calls an unfounded &quot;smear.&quot; Analysts cited by CNBC say the episode, coming days after Democrats swept the Nov. 3 midterms and ahead of a Trump-Xi meeting at APEC in Shenzhen on Nov. 18-19, could harden U.S. export controls on chip sales to China.

rss · CNBC Finance · Nov 13, 02:56

**「Background」** Washington began restricting Nvidia&\#x27;s sales of advanced AI chips to China in 2022, and the Trump administration eased many Biden-era limits in 2025, including allowing sales of older H200 chips in exchange for a 25% tariff. Congress is separately trying to attach tighter export-control measures to this year&\#x27;s National Defense Authorization Act.

**「Impact」** Analysts expect the affair to weaken Nvidia&\#x27;s lobbying against U.S. export controls, which could mean tighter limits on chipmakers&\#x27; China sales and lower revenue for U.S. semiconductor firms, while Beijing has warned it could restrict rare-earth or chipmaking-material exports in return.

<details><summary>References</summary>
<ul>
<li><a href="https://www.axios.com/2026/11/11/trump-lutnick-nvidia-china-chip-export-controls">Trump backed Nvidia chip controls aimed at China 3 times as Lutnick...</a></li>
<li><a href="https://www.cnbc.com/2026/11/11/nvidia-jensen-huang-congress-resign-ai-chips.html">Jensen Huang affair rocks D.C., brings calls from Congress to resign</a></li>
<li><a href="https://www2.itif.org/2025-semiconductor-export-controls.pdf">Decoupling Risks: How Semiconductor Export Controls Could...</a></li>

</ul>
</details>

**Tags**: `#US-China relations`, `#Nvidia`, `#export controls`, `#semiconductors`, `#geopolitical risk`

---

<a id="item-finance-news-2"></a>
### [礼来口服减重药在华获批，成为中国首个口服 GLP-1 减重疗法](https://www.reuters.com/business/healthcare-pharmaceuticals/china-approves-eli-lillys-weight-loss-pill-orforglipron-2026-11-12/) ⭐️ 8.0/10

中国国家药监局于11月12日批准礼来公司的每日一次口服GLP-1减重药奥氟格列隆（orforglipron，商品名穆优达）作为1类新药上市，用于肥胖或超重且伴有至少一种体重相关合并症的成人，这是中国首个获批的口服GLP-1减重药。礼来未公布该药的价格和上市时间，其2型糖尿病适应症仍在审评中。

telegram · zaihuapd · Nov 12, 10:09

**「Background」** Until now, the GLP-1 weight-loss drugs on the Chinese market — including those from Novo Nordisk and Innovent — were given as weekly injections, so a once-daily pill offers patients a different way to take the treatment. Reuters reported the approval gives Lilly an early advantage over Danish rival Novo Nordisk in the world&\#x27;s second-largest pharmaceutical market.

**「Impact」** The approval gives Eli Lilly an early edge over Novo Nordisk in China&\#x27;s weight-loss market, where orforglipron will compete against weekly injectable GLP-1 treatments from Novo Nordisk, Pfizer and China&\#x27;s Innovent Biologics. Price and launch timing have not been announced, so patient access and the scale of any commercial advantage remain unknown.

<details><summary>References</summary>
<ul>
<li><a href="https://www.reuters.com/business/healthcare-pharmaceuticals/china-approves-eli-lillys-weight-loss-pill-orforglipron-2026-11-12/">Eli Lilly becomes first drugmaker to have a GLP-1 weight-loss ...</a></li>
<li><a href="https://pharmaphorum.com/news/lilly-beats-novo-china-oral-glp-1-obesity">Lilly beats Novo to China with an oral GLP-1 for obesity</a></li>
<li><a href="https://www.reuters.com/business/healthcare-pharmaceuticals/china-approves-eli-lillys-weight-loss-pill-orforglipron-2026-11-12/">Eli Lilly becomes first drugmaker to have a GLP-1 weight-loss ...</a></li>
<li><a href="https://seekingalpha.com/news/4671225-china-approves-eli-lillys-glp-1-weight-loss-pill-giving-it-lead-over-novo---report">China approves Eli Lilly&#x27;s GLP-1 weight-loss pill, giving it ...</a></li>
<li><a href="https://www.pharmaceutical-technology.com/news/eli-lilly-oral-glp1-ra-foundayo-nmpa-approval-weight-management/">Eli Lilly beats Novo to oral China GLP-1RA market on NMPA ...</a></li>

</ul>
</details>

**Tags**: `#pharmaceuticals`, `#GLP-1`, `#regulatory approval`, `#Eli Lilly`, `#China healthcare`

---