---
layout: default
title: "Horizon Summary: 2026-11-21 (EN)"
date: 2026-11-21
lang: en
---

> From 39 items, 14 important content pieces were selected

---

**Technology News**
1. [Inkling 2 Mini: open-weights small model with looped transformer](#item-tech-news-1) ⭐️ 8.0/10
2. [Anthropic mathematician claims Claude-assisted proof of Riemann Hypothesis](#item-tech-news-2) ⭐️ 8.0/10
3. [Unverified finite-time Navier–Stokes blow-up claim posted on GitHub](#item-tech-news-3) ⭐️ 8.0/10
4. [KVM CVE-2026-99312 Exposes AMD Host Memory to Guests](#item-tech-news-4) ⭐️ 8.0/10
5. [TSMC Reportedly Halts 16nm and Below Orders From Chinese Firms](#item-tech-news-5) ⭐️ 8.0/10
6. [SEC reportedly probes Nvidia over potential accounting issues](#item-tech-news-6) ⭐️ 7.0/10
7. [Signal Moves to Restrict AI Agents From Capturing Private Data](#item-tech-news-7) ⭐️ 7.0/10
8. [Terry Tao on Navier–Stokes Singularities, GRH and Proof Checking](#item-tech-news-8) ⭐️ 7.0/10
9. [US Tightens Chip Export Rules as India Seeks AI Compute Spillover](#item-tech-news-9) ⭐️ 7.0/10
10. [Apple reportedly developing proactive AI agent for coding and app control](#item-tech-news-10) ⭐️ 7.0/10

**Technology Blog**
1. [Output Caching Misses Most Agent Token Spend](#item-tech-blog-1) ⭐️ 6.0/10

**Financial News**
1. [Warsh avoids rate guidance while Fed colleagues speak out more](#item-finance-news-1) ⭐️ 7.0/10
2. [U.S. companies shift from buybacks to net equity issuance](#item-finance-news-2) ⭐️ 7.0/10
3. [Beijing Proposes Barring Deposit Deductions for Normal Rental Wear](#item-finance-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Inkling 2 Mini: open-weights small model with looped transformer](https://thinkingmachines.ai/news/inkling-2-mini/) ⭐️ 8.0/10

Inkling 2 Mini, an open-weights small model, has been released with a reported looped-transformer architecture aimed at local inference. Early community tests report about 27 tokens/s decode on a Ryzen 395 using llama.cpp&\#x27;s Vulkan backend and roughly 10 tokens/s on a 32 GB M1 Pro with a q4 XL quant. Those throughput figures and comparisons to Qwen3.8-27B are community reports rather than independent verification, and early llama.cpp use involved unmerged pull requests plus, in one report, a small patch for a claimed ~30% speedup.

hackernews · jasondavies · Nov 20, 20:12 · [Discussion](https://news.ycombinator.com/item?id=50581260)

**「Background」** A looped transformer reuses its middle layers instead of stacking a new layer for every pass, allowing the model to spend more computation per token; Thinking Machines says Inkling 2 Mini loops its middle layers to reason more per token and reach answers in fewer tokens. Artificial Analysis describes the release as a 26B-total, 5.4B-active mixture-of-experts model.

**「Local inference depends on unmerged patches」** Developers can run the open-weights model locally through llama.cpp or Ollama using community GGUF builds, but the reported throughput figures depend on fixes that are not yet in the mainline: one tester needed four pending llama.cpp pull requests plus a small graph patch for roughly a 30% speed boost to reach about 27 tokens/s on a Ryzen 395 with Vulkan. Another tester on an M1 Pro with 32 GB saw about 10 tokens/s at q4 with mixed coding results, so teams should benchmark quality and speed on their own hardware rather than assume the published benchmark claims transfer.

**「Community discussion」** Commenters were enthusiastic but conditional: one called the benchmark results “bonkers good” if they hold up in real-world use, while another reported a solid Python coding result but a failure on a harder coin-identification test after about 12,000 tokens. Commenters also debated the significance of the looped design, with one predicting most open models will adopt it and raising questions about safety and interpretability.

<details><summary>References</summary>
<ul>
<li><a href="https://thinkingmachines.ai/news/inkling-2-mini/">Introducing Inkling 2 Mini - Thinking Machines Lab</a></li>
<li><a href="https://artificialanalysis.ai/articles/inkling-2-mini">Thinking Machines has released Inkling 2 Mini, an open ...</a></li>

</ul>
</details>

**Tags**: `#open-weight models`, `#looped transformers`, `#local inference`, `#llama.cpp`, `#model efficiency`

---

<a id="item-tech-news-2"></a>
### [Anthropic mathematician claims Claude-assisted proof of Riemann Hypothesis](https://alpo.ge/remark.pdf) ⭐️ 8.0/10

On November 20, 2026, Levent Alpöge published a note claiming that he and Claude discovered a proof of the Riemann Hypothesis that extends to the Generalized Riemann Hypothesis and has been formalized in Lean without assumptions. The accompanying Lean development is described in comments as about 1.3 GB and roughly 15 million lines, while the source summary says the detailed proof manuscript exceeds 250,000 pages. The claim has not been independently verified or peer reviewed; the item presents Alpöge&\#x27;s assertion, and commenters point to checks that were still in progress.

hackernews · iamronaldo · Nov 20, 14:16 · [Discussion](https://news.ycombinator.com/item?id=50574968)

**「Background」** The Riemann Hypothesis, posed in 1859, is a long-unproven claim about how prime numbers are distributed; the Generalized Riemann Hypothesis extends the same kind of claim to a broader setting. Lean, the proof assistant Alpöge says he used, is designed to machine-check each step of a formal argument, which is why the posted Lean archive is central to assessing the claim.

**「Verification burden shifts to independent checkers」** Because the argument was released as a machine-checkable Lean development rather than a paper alone, the immediate consequence is that mathematicians can audit it directly: MIT&\#x27;s Andrew Sutherland has started running checks, and his page reported on 2026-11-20 that the published Lean source compiles without errors, with results to be updated as the remaining checks finish. The practical caveat for anyone acting on the claim is that a clean build is not acceptance — the development commenters describe as roughly 1.3 GB and ~15 million lines takes substantial compute to rebuild, so the result stays unverified until those independent checks complete.

**「Community discussion」** Commenters focused on the scale and implications of the claimed proof: one posted commands for downloading a 14-part Lean archive and measured it at 1.3 GB and about 15 million lines, while another linked a purported human proof and noted that Terence Tao had recently been skeptical that current AI could solve the Riemann Hypothesis. One commenter asserted that the proof had been formally verified in multiple ways, citing an MIT page of checks, but that is a community-reported claim rather than independent confirmation.

<details><summary>References</summary>
<ul>
<li><a href="https://www.scientificamerican.com/article/anthropic-mathematician-claims-to-prove-riemann-hypothesis-most-famous-problem-in-all-of-math/">Anthropic mathematician claims to prove Riemann hypothesis , most...</a></li>
<li><a href="https://math.mit.edu/~drew/grh/">RH Lean proof: verification files - MIT Mathematics</a></li>
<li><a href="https://thebostonreport.com/2026/11/20/claimed-riemann-hypothesis-proof-mit-lean/">MIT Checks Claimed Riemann Hypothesis Proof | The Boston Report</a></li>

</ul>
</details>

**Tags**: `#formal verification`, `#Lean theorem prover`, `#Riemann Hypothesis`, `#mathematics`, `#unverified claim`

---

<a id="item-tech-news-3"></a>
### [Unverified finite-time Navier–Stokes blow-up claim posted on GitHub](https://github.com/tristanbuckmaster/navier-stokes/) ⭐️ 8.0/10

A GitHub repository titled &quot;Finite-time blow-up for the Navier–Stokes equations&quot; was posted to Hacker News. The supplied item contains only the link and discussion, with no proof text, paper, or independent confirmation, so the asserted finite-time blow-up remains unverified.

hackernews · trotro · Nov 20, 15:34 · [Discussion](https://news.ycombinator.com/item?id=50576232)

**「Background」** The Navier–Stokes existence and smoothness problem, one of the Millennium Prize Problems, asks whether smooth three-dimensional initial data always yield smooth solutions for all time; a finite-time blow-up would settle it in the negative. On 8 September 2026 OpenAI announced a proof, with a Lean formalization, that the equations can develop a singularity in finite time \(tool-3-3\), a result commenters here describe as relying on a carefully designed external forcing term. The repository discussed in this item presents a paper and a Lean 4 formalization aimed at the unforced case \(tool-1-2\).

**「Community discussion」** Commenters debated whether the claim concerns the unforced equations, with one saying it is more &quot;realistic&quot; than a purported OpenAI result that relied on a carefully designed external force. Others asked whether a simulation could show the blow-up in real time and whether a physical demonstration could make the behavior intuitive; these are reactions, not confirmation of the claim.

<details><summary>References</summary>
<ul>
<li><a href="https://hotrepo.ai/tristanbuckmaster/navier-stokes">tristanbuckmaster/navier-stokes: Lean 4 formalization of a ...</a></li>
<li><a href="https://openai.com/index/navier-stokes-solution/">On the Navier–Stokes Millennium Prize Problem | OpenAI</a></li>

</ul>
</details>

**Tags**: `#Navier–Stokes equations`, `#mathematics`, `#fluid dynamics`, `#research claim`, `#Hacker News`

---

<a id="item-tech-news-4"></a>
### [KVM CVE-2026-99312 Exposes AMD Host Memory to Guests](https://thehackernews.com/2026/11/new-linux-kvm-flaw-cve-2026-99312-lets.html) ⭐️ 8.0/10

The Linux KVM vulnerability CVE-2026-99312 lets a guest on an AMD host with nested virtualization enabled read host memory; researchers demonstrated reading about 127 GB of host memory from a VM on DigitalOcean. The flaw was fixed upstream on November 18 in stable kernel 7.3.5 and related releases, but Debian, Ubuntu, and other distribution kernels remain unpatched, according to the report. Until those kernels are updated, affected operators can mitigate the exposure by disabling nested virtualization.

telegram · zaihuapd · Nov 20, 14:23

**「How the KVM flaw works」** KVM is the Linux kernel&\#x27;s hypervisor, and nested virtualization lets a guest run its own virtual machines on top of it. Red Hat&\#x27;s advisory describes the mechanism: KVM unconditionally resets the MMU context when it emulates an INIT instruction even while paging is disabled, which can leave a nested VM running with a stale context that still references structures from a higher-level virtual machine; Red Hat rates the issue Moderate because exploitation requires nested virtualization on AMD-based hosts plus specific guest execution conditions.

**「What operators should do」** Administrators of AMD hosts with nested virtualization enabled face a choice between exposure and lost functionality: until their distribution ships the fix, the practical mitigation is to disable nested virtualization, which breaks any workload that depends on running VMs or containers with hardware virtualization inside a guest. DigitalOcean, where the 127 GB read was demonstrated, has published the patched kernels it deployed, so tenants on that provider can check their hosts&\#x27; status rather than waiting on distro backports.

<details><summary>References</summary>
<ul>
<li><a href="https://access.redhat.com/security/cve/cve-2026-99312">CVE-2026-99312 - Red Hat Customer Portal</a></li>
<li><a href="https://app.opencve.io/cve/CVE-2026-99312">CVE-2026-99312 - Vulnerability Details - OpenCVE</a></li>
<li><a href="https://www.digitalocean.com/blog/cve-2026-99312-kvm-patch">Virtualization , Responsible Disclosure, and CVE - 2026 - 99312</a></li>
<li><a href="https://thehackernews.com/2026/11/new-linux-kvm-flaw-cve-2026-99312-lets.html">Linux KVM Flaw CVE - 2026 - 99312 Lets Guest VMs Access Host...</a></li>

</ul>
</details>

**Tags**: `#KVM`, `#Linux kernel`, `#CVE`, `#virtualization security`, `#AMD`

---

<a id="item-tech-news-5"></a>
### [TSMC Reportedly Halts 16nm and Below Orders From Chinese Firms](https://appleinsider.com/articles/26/11/20/apple-supplier-tsmc-cuts-off-china-chip-orders-amid-tighter-export-controls) ⭐️ 8.0/10

TSMC has reportedly told customers it is suspending orders from Chinese companies for 16nm-and-below processes, citing tighter U.S. export rules that require a U.S. license or exemption before shipment. The reported change would leave Chinese firms restricted to older nodes such as 28nm and 40nm and potentially unable to obtain the high-bandwidth memory used in AI data-center systems. Previously TSMC could assess whether a customer&\#x27;s design qualified for an exemption; customers must now apply in advance, and the U.S. approved list includes Apple, AMD and Nvidia but no Chinese companies. TSMC said it will comply with the rules; the report has not been independently verified.

telegram · zaihuapd · Nov 21, 02:01

**「Background」** Under the tightened U.S. export-control rule, Chinese customers must obtain a U.S. license or exemption before TSMC can fill orders at 16nm and more advanced nodes; previously, TSMC could assess for itself whether a customer’s design qualified. Reports describing the change say affected Chinese customers were told to stop placing orders at 16nm and below unless they hold U.S. export licenses.

**「Impact」** For Chinese chip designers, the reported pause adds a licensing gate: 16nm-and-below orders cannot proceed without a U.S. license or exemption, leaving 28nm and 40nm as the available TSMC nodes and, according to the report, cutting off the high-bandwidth memory needed for AI data-center chips. The suspension may also extend to consumer-chip shipments, not just AI processors.

<details><summary>References</summary>
<ul>
<li><a href="https://finance.yahoo.com/technology/ai/articles/tsmc-halting-china-chip-orders-131332877.html?fr=sycsrp_catchall">TSMC Is Halting Some China Chip Orders as a New U.S. Rule ...</a></li>
<li><a href="https://appleinsider.com/articles/26/11/20/apple-supplier-tsmc-cuts-off-china-chip-orders-amid-tighter-export-controls">TSMC has suspended some chip orders amid tighter export controls</a></li>
<li><a href="https://www.trendforce.com/news/2026/11/20/news-tsmc-samsung-reportedly-pause-china-consumer-chip-shipments-under-new-u-s-rules-16nm-orders-affected/">[News] TSMC , Samsung Reportedly Pause China Consumer Chip ...</a></li>

</ul>
</details>

**Tags**: `#semiconductor export controls`, `#TSMC`, `#China`, `#AI hardware`, `#supply chain`

---

<a id="item-tech-news-6"></a>
### [SEC reportedly probes Nvidia over potential accounting issues](https://www.marketscreener.com/news/us-sec-s-nvidia-probe-is-examining-potential-accounting-issues-sources-say-ce785ed3dd8ff627) ⭐️ 7.0/10

The U.S. SEC is reportedly examining potential accounting issues at Nvidia, according to sources cited in a MarketScreener report. The supplied item does not include formal allegations, the probe&\#x27;s scope or timeline, or a response from Nvidia, so the examination and its substance remain unconfirmed. The report is attributed to unnamed sources rather than an SEC or Nvidia disclosure.

hackernews · ftchd · Nov 20, 20:22 · [Discussion](https://news.ycombinator.com/item?id=50581438)

**「Earlier regulatory scrutiny」** The reported SEC scrutiny comes alongside other regulatory pressure on Nvidia: Reuters has reported that the Justice Department was reviewing the company&\#x27;s $12.9 billion deal to buy Hugging Face as part of a broader antitrust investigation into its acquisitions and practices.

**「Market fallout」** Nvidia investors are already absorbing the immediate cost: the reported SEC accounting probe coincided with a selloff that erased roughly $500 billion in market value in a single day and left the stock about 48% below its October record, according to market reports. The rapid repricing shows how quickly the reported scrutiny has translated into losses even before any findings or charges are announced.

**「Community Discussion」** Commenters focused on governance and accounting risk, with one questioning why the board would make CFO Colette Kress interim CEO if it suspected accounting problems, and another arguing the report extends existing concerns about circular financing and renegotiated neocloud deals. These are speculative opinions; the supplied item provides no confirmed details about the SEC&\#x27;s scope or findings.

<details><summary>References</summary>
<ul>
<li><a href="https://www.investing.com/news/economy-news/exclusiveus-secs-nvidia-probe-is-examining-potential-accounting-issues-sources-say-5042460">Nvidia ’s accounting is a focus of US SEC investigation, sources say...</a></li>
<li><a href="https://finance.yahoo.com/markets/article/nvidia-stock-extends-25-trillion-rout-as-sec-probe-reportedly-investigates-its-accounting-194945274.html?fr=sycsrp_catchall">Nvidia stock extends $2.7 trillion rout as SEC probe ...</a></li>
<li><a href="https://www.fool.com/investing/2026/11/20/nvidia-stock-plunge-wipes-out-nearly-usd500-billion-in-one-day-as-sec-reportedly-probes-its-accounting/">Nvidia Stock Plunge Wipes Out Nearly $500 Billion in One Day ...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#SEC investigation`, `#accounting`, `#tech industry`, `#regulatory risk`

---

<a id="item-tech-news-7"></a>
### [Signal Moves to Restrict AI Agents From Capturing Private Data](https://signal.org/blog/protecting-your-privacy/) ⭐️ 7.0/10

Signal published a blog post describing its effort to restrict AI agents and mobile operating-system platforms from capturing private data, including chats. The available material does not include the post&\#x27;s technical findings, so it is not clear whether this is a shipped protection, a proposed mitigation, or an ongoing investigation. Commenters characterized the post as progress and relayed Signal&\#x27;s statement that it is “cautiously optimistic” about some measures, but the excerpt does not specify which platforms, permissions, or mechanisms are involved.

hackernews · dotcoma · Nov 20, 09:42 · [Discussion](https://news.ycombinator.com/item?id=50572348)

**「Background」** Signal is targeting a specific class of risk: AI agents built into mobile operating systems that can use system-level access to reach into otherwise protected apps and capture or store their data. Signal has framed the integration of such agents into the OS, without common-sense remedies, as a threat to privacy at the application layer, which is the premise for its move to restrict the latest agents from capturing or storing Signal data.

**「Impact」** For Signal users, the concern raised in discussion is indirect exposure: a chat could be captured through an AI-enabled app on a contact&\#x27;s device even if the user has not installed one, so protection depends on both parties&\#x27; app environments and on OS-level controls. Users who rely on Signal for sensitive conversations may therefore need to treat the other party&\#x27;s device configuration as part of their threat model.

**「Community Discussion」** Commenters welcomed the effort but disagreed on the remedy: some urged Signal to publish its forensic findings so smaller developers could benefit, while others said users need OS-level control, warnings about spyware, and alternatives such as GrapheneOS or Linux. A separate thread reported that Signal&\#x27;s spam protection makes VPN use difficult, arguing that forcing users to reveal IP addresses undermines privacy for journalists and sources.

<details><summary>References</summary>
<ul>
<li><a href="https://signal.org/blog/protecting-your-privacy/">Signal is Serious About Protecting Your Privacy</a></li>
<li><a href="https://signal.org/blog/">Signal &gt;&gt; Blog</a></li>

</ul>
</details>

**Tags**: `#privacy`, `#mobile security`, `#AI agents`, `#Signal`, `#platform access`

---

<a id="item-tech-news-8"></a>
### [Terry Tao on Navier–Stokes Singularities, GRH and Proof Checking](https://terrytao.wordpress.com/2026/11/20/unforced-euler-singularity-unforced-navier-stokes-singularity-and-the-generalized-riemann-hypothesis/) ⭐️ 7.0/10

Terry Tao published a blog post on unforced Navier–Stokes singularities and the generalized Riemann Hypothesis, prompting a Hacker News discussion focused on AI-assisted proof verification and Lean theorem proving. Commenters cited a claim that two independent kernels accepted a result, making kernel-bug exploitation unlikely, while others questioned how a large Lean build can be checked to prove the intended statement rather than something trivial. The supplied item contains no article body, so the post&\#x27;s specific mathematical claims and any new results cannot be independently assessed here.

hackernews · archon1410 · Nov 20, 17:21 · [Discussion](https://news.ycombinator.com/item?id=50578358)

**「Background」** Tao’s November 20, 2026 post follows his October 4, 2026 expository guest post on classical solutions and singularity formation in incompressible fluids, which treated singularity formation in the Euler and Navier–Stokes equations. Tao’s own notes describe the original Navier–Stokes case as supercritical, placing global regularity beyond most known methods.

**「Verification gap」** For researchers using Lean to check AI-generated proofs, the practical requirement is to audit the formal statement as well as the proof term: a passing kernel check shows only that the proof establishes the encoded theorem, not that the encoding matches the intended informal claim. Teams adopting this workflow should therefore treat the informal-to-formal translation as a separate verification step.

**「Community Discussion」** Commenters described the moment as both exciting and frightening for mathematical research careers, with one asking how new abstractions and concepts are created rather than merely verified. Another raised a practical verification concern: whether a Lean build that passes actually proves the intended claim, rather than a trivial or mismatched statement.

<details><summary>References</summary>
<ul>
<li><a href="https://terrytao.wordpress.com/tag/navier-stokes-equations/">Navier-Stokes equations – What&#x27;s new</a></li>
<li><a href="https://terrytao.wordpress.com/2026/10/04/on-classical-solutions-and-singularity-formation-in-incompressible-fluids/">On classical solutions and singularity formation in ...</a></li>
<li><a href="https://mathoverflow.net/questions/513540/should-we-trust-ai-generated-formal-proofs-in-lean-4">Should we trust AI-generated formal proofs in Lean 4?</a></li>
<li><a href="https://mlcrypto.mit.edu/course/scribe-notes/lec14_scribe.pdf">Lecture 14: Lean: A Different Take on Verification</a></li>

</ul>
</details>

**Tags**: `#mathematics`, `#Navier-Stokes`, `#Riemann Hypothesis`, `#Lean theorem proving`, `#AI-assisted research`

---

<a id="item-tech-news-9"></a>
### [US Tightens Chip Export Rules as India Seeks AI Compute Spillover](https://www.bloomberg.com/news/articles/2026-11-20/nvidia-scandal-fallout-india-ai-yotta-ambani-adani-am-intelligence-e2e-networks) ⭐️ 7.0/10

A Telegram digest of Bloomberg reporting says the US is tightening restrictions on advanced chip exports to Malaysia, Thailand, and Singapore, prompting India’s AI sector to try to capture diverted demand. Yotta says it will add about 100,000 GPUs over the next year—equivalent to roughly 10% of India’s existing compute, according to the digest. India currently has 153 data centers, ranking 14th globally, while Reliance has committed up to $110 billion and Adani $100 billion to AI infrastructure; the sector still faces shortages of compute infrastructure and limited capital.

telegram · zaihuapd · Nov 20, 07:31

**「Background」** India’s planned AI expansion is being measured against a relatively modest domestic base: the source cites 153 data centers, ranking 14th globally, and says the country has been held back by compute-infrastructure shortages and limited capital. The item hinges on whether tighter US export rules for Malaysia, Thailand, and Singapore redirect advanced-chip demand toward India, but it does not specify the rule’s legal scope or timing.

**「Impact」** Indian AI developers and data-center operators should treat power and skills as the gating items for the announced GPU buildout: Yotta’s plan to add about 100,000 GPUs—roughly 10% of India’s current compute—still depends on electricity delivery, which one industry analysis calls the biggest constraint, and on hiring from a market facing a reported shortfall of roughly 1–1.4 million AI professionals. The practical action is to secure power contracts and AI staffing alongside GPU procurement, rather than assume the new hardware alone will translate into available capacity.

<details><summary>References</summary>
<ul>
<li><a href="https://www.ziromarket.com/blog/india-data-center-boom-2026">India Data Center Boom 2026 | Who Benefits | Ziro Market</a></li>
<li><a href="https://www.linkedin.com/posts/vineethv_india-just-switched-on-38000-sovereign-gpus-activity-7425772836012822528-98dR">India Deploys 38,000 GPUs , But AI Talent Shortfall Looms | LinkedIn</a></li>

</ul>
</details>

**Tags**: `#AI infrastructure`, `#export controls`, `#India`, `#GPUs`, `#data centers`

---

<a id="item-tech-news-10"></a>
### [Apple reportedly developing proactive AI agent for coding and app control](https://www.bloomberg.com/news/articles/2026-11-19/apple-is-working-on-ai-agent-for-device-control-apps-browsing-and-coding) ⭐️ 7.0/10

Bloomberg reports, based on Apple job postings added this week, that Apple is recruiting a senior engineering manager to lead development of a &quot;proactive AI agent&quot; that could write code, browse the web and operate apps on the user&\#x27;s behalf. The report puts the earliest launch at late 2027 and describes the project as still early-stage, so scope and timing are unconfirmed plans rather than a shipped product. The same account says macOS 27.3 introduces a warning screen and raises the number of steps a third-party agent must clear to obtain control of a Mac from four to fourteen, while competitors including Meta&\#x27;s Muse and OpenAI have already released similar agents.

telegram · zaihuapd · Nov 20, 08:59

**「Background」** “Proactive” AI agents are designed to carry out multi-step tasks — such as writing code, browsing the web, and operating apps — with less direct user prompting than a chatbot. According to the source, Apple is recruiting a senior engineering manager for the effort while macOS 27.3 adds a warning page and increases the number of steps for third-party agents to obtain Mac control from four to fourteen, even as Meta and OpenAI already offer comparable agents.

**「Impact」** Developers building device-control agents for the Mac would face a markedly longer permission flow — fourteen steps instead of four under macOS 27.3 — adding friction to shipping general-purpose automation even before Apple&\#x27;s own agent arrives. That makes the permission design, not just the agent&\#x27;s capabilities, the near-term constraint for third-party tools.

**Tags**: `#Apple`, `#AI agents`, `#macOS`, `#automation`, `#platform policy`

---

## Technology Blog

<a id="item-tech-blog-1"></a>
### [Output Caching Misses Most Agent Token Spend](https://seangoedecke.com/why-output-caching-doesnt-work/) ⭐️ 6.0/10

rss · Sean Goedecke · Nov 21, 00:00

**「Background」** LLM inference already caches inputs in the KV cache so the entire conversation history is not recomputed on every message. The author asks whether outputs can be cached similarly, since coding and research agents often repeat code snippets or evidence documents in their responses.

**「Solution」** One proposed mechanism is to train or prompt a model to emit references such as “src/script.py:12-15” or point to segments of its own conversation history, which the harness could transparently expand. The author rejects this as largely futile because it optimizes only visible output. In his own agent histories, visible output is roughly 6% of output tokens, while reasoning accounts for 50% and tool calls 44%. By Amdahl’s law, even saving two-thirds of visible output would cut only about 4% of total output tokens. He is only moderately confident that frontier models rarely repeat themselves in chain of thought, though he notes some early open reasoning models do while also using far more tokens. Tool-call repetition remains an open question. The larger target is the invisible 94%, which depends on intelligence: a model costing 5x more per token can be cheaper overall if it reaches the answer with 6x fewer tokens.

**「Takeaway」** Output caching attacks too small a share of agent token spend to matter much. The author’s broader point is that reducing reasoning and tool-call tokens—often through a smarter model whose lower total token count outweighs its higher per-token price—is the more consequential lever.

**Tags**: `#LLM inference economics`, `#output caching`, `#Amdahl&\#x27;s law`, `#agent token usage`, `#reasoning models`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Warsh avoids rate guidance while Fed colleagues speak out more](https://www.cnbc.com/2026/11/20/warsh-fed-forward-guidance-rate-hikes.html) ⭐️ 7.0/10

Federal Reserve officials are publicly debating interest-rate increases more often than in any comparable period since the start of 2025, according to a Bank of America analysis, while Chairman Kevin Warsh declines to signal where policy is headed. Traders are pricing a 100% chance of at least a quarter-point hike at the December meeting, according to CME Group&\#x27;s FedWatch.

rss · CNBC Finance · Nov 20, 21:10

**「Background」** Earlier in his tenure, Warsh pushed to curb Fed communication—proposing fewer FOMC meetings and less public commentary, then cutting the policy statement to 132 words and dropping forward guidance, which is an explicit signal about future rate moves.

**「Impact」** Investors holding rate-sensitive assets are directly affected: Bank of America economist Aditya Bhave says the competing Fed messages are producing &quot;undue rates volatility,&quot; even as a Treasury-market measure of five-year forward inflation expectations has fallen to its lowest since April.

<details><summary>References</summary>
<ul>
<li><a href="https://www.financialexpress.com/market/global-market-pulse/why-fed-chair-warsh-scrapped-forward-guidance-in-a-132-word-pivot/4272071/">Why Fed Chair Warsh scrapped forward guidance in a 132-word ...</a></li>
<li><a href="https://cryptobriefing.com/fed-chair-warsh-communication-reforms/">Federal Reserve Chair Kevin Warsh proposes communication ...</a></li>

</ul>
</details>

**Tags**: `#Federal Reserve`, `#monetary policy`, `#interest rates`, `#FOMC`, `#forward guidance`

---

<a id="item-finance-news-2"></a>
### [U.S. companies shift from buybacks to net equity issuance](https://www.cnbc.com/2026/11/20/equity-issuance-bull-market-problem.html) ⭐️ 7.0/10

U.S. companies have shifted from repurchasing shares in 2024 to issuing them now, with net new equity issuance equal to 3.1% of total market capitalization as of late last week, according to an Acadian Asset Management analysis.

rss · CNBC Finance · Nov 20, 14:15

**「Background」** Buybacks reduce the number of shares available for trading and can support prices and lift earnings per share by shrinking that denominator; the reversal adds supply the market must absorb.

**「Impact」** Existing shareholders in companies issuing new stock, including Oracle and Meta, face dilution as more shares are sold, while the broader market must absorb that added supply.

**Tags**: `#equity issuance`, `#buybacks`, `#bull market`, `#AI capex`, `#IPO market`

---

<a id="item-finance-news-3"></a>
### [Beijing Proposes Barring Deposit Deductions for Normal Rental Wear](https://mp.weixin.qq.com/s/PmGxh5knIyxiBRhpRoJnoQ) ⭐️ 7.0/10

Beijing’s housing and market regulators on Nov. 20 opened public comment on a draft model residential lease that would bar landlords from deducting deposits for normal wear and tear from ordinary use. The draft would also require rental companies that sublet homes to place tenant deposits and rent into supervised accounts.

telegram · zaihuapd · Nov 20, 13:46

**「Background」** Beijing had already sought public comment in July 2025 on a draft notice regulating individuals who sublet rented homes \(known locally as &quot;second landlords&quot;\), part of a wider push to tighten order in the rental market \(tool-1-2\). A &quot;model text&quot; is a contract template issued by government departments for landlords and tenants to use voluntarily; it is not itself mandatory.

<details><summary>References</summary>
<ul>
<li><a href="https://house.cnr.cn/rdtj/20250710/t20250710_527254499.shtml">北 京 加强个人“二 房 东” 监 管 促进 住 房 租 赁 市场健康发展_央广网</a></li>

</ul>
</details>

**Tags**: `#北京住房租赁`, `#押金监管`, `#租户权益`, `#政策征求意见`, `#住房租赁市场`

---