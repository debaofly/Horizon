---
layout: default
title: "Horizon Summary: 2026-11-14 (EN)"
date: 2026-11-14
lang: en
---

> From 41 items, 11 important content pieces were selected

---

**Technology News**
1. [Scaling a 1T-parameter MoE on TorchTitan to 1,300 tokens/s per GPU](#item-tech-news-1) ⭐️ 8.0/10
2. [orcasairband.com live-transcribes airband radio from KORS with dual GPUs](#item-tech-news-2) ⭐️ 7.0/10
3. [FAA Issues Nationwide Ground Stop, Later Reported Lifted](#item-tech-news-3) ⭐️ 7.0/10
4. [Haskell ecosystem technical vision sparks debate on tooling and AI](#item-tech-news-4) ⭐️ 7.0/10
5. [Python early contributor Tim Peters dies at 74](#item-tech-news-5) ⭐️ 7.0/10
6. [Microsoft 365 outage hits Outlook, Teams and Copilot worldwide](#item-tech-news-6) ⭐️ 7.0/10
7. [DeepSeek opens app API for search, files, and voice](#item-tech-news-7) ⭐️ 7.0/10
8. [OpenAI launches ChatGPT Wallet for agent payments with Visa, Mastercard, Amex](#item-tech-news-8) ⭐️ 7.0/10

**Financial News**
1. [Cantor Fitzgerald trimmed its reported Nvidia stake as Washington scrutinized the chipmaker](#item-finance-news-1) ⭐️ 8.0/10
2. [Goolsbee Says Fed Has &\#x27;Work to Do&\#x27; on Inflation After PPI Rise](#item-finance-news-2) ⭐️ 7.0/10
3. [Jensen Huang resigns from Nvidia; analysts see tighter China export controls](#item-finance-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Scaling a 1T-parameter MoE on TorchTitan to 1,300 tokens/s per GPU](https://www.reddit.com/r/MachineLearning/comments/1xvce5h/scaling_to_1t_moe_on_torchtitan_p/) ⭐️ 8.0/10

A Reddit write-up from a team working with TorchTitan and PyTorch maintainers reports training a ~1T-parameter MoE on 384 GH200 GPUs at about 1,300 tokens/s per GPU, a 14× improvement over its starting point. The setup uses 384-way FSDP with 4-way expert parallelism kept inside each node and skips pipeline parallelism; on JUPITER, the authors say InfiniBand&\#x27;s ~25 GB/s per GPU made communication the dominant cost, with 68 of an initial 84-second step spent waiting on the network. The reported gains come from full activation checkpointing \(4×\), offloading checkpoint activations to Grace, Muon with whole-expert FlexShard sharding, moving Newton-Schulz to the GPU \(optimizer step from 42 s to ~2 s, +35% throughput\), attention-cost bucketing \(+13%\), FP8 expert all-gather \(+18%\), and stream-aware allocator changes \(+21%, 13.5 GiB lower peak reserved memory\). These are the team&\#x27;s reported results from a community post, not an independent benchmark; group-limited routing added 7%, but the authors say early runs suggest it may hurt training and that the jury is still out.

reddit · r/MachineLearning · /u/f14-bertolotti · Nov 13, 16:28

**「What TorchTitan and GH200 are」** TorchTitan is the PyTorch project&\#x27;s open-source, PyTorch-native platform for large-scale distributed training, packaging techniques such as FSDP and expert parallelism into a single readable codebase. The GH200 is NVIDIA&\#x27;s Grace Hopper Superchip, which pairs a Hopper GPU with a Grace CPU over a high-bandwidth chip-to-chip link, and JUPITER is the supercomputer built from them. That combination is what makes the post&\#x27;s configuration — hundreds of GH200s sharded via FSDP with expert parallelism kept inside each node, plus optimizer state offloaded to Grace — the natural design to evaluate.

**「Impact」** Developers training large MoE models on GH200-class systems can treat the report as a checklist of bottlenecks: keep expert all-to-all node-local, avoid pipeline bubbles, shard experts whole for Muon, and watch for caching-allocator pools on side streams. The reported 13.5 GiB memory reduction and 21% throughput gain from moving allocations onto the compute stream is a concrete compatibility concern for FSDP2 users, because the fix relied on the private \`unshard\_async\_op\` flag that the authors say is on its way to becoming a public API.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/pytorch/torchtitan">GitHub - pytorch / torchtitan : A PyTorch native platform for training ...</a></li>
<li><a href="https://arxiv.org/pdf/2410.06511">TorchTitan : One-stop PyTorch native solution for production ready...</a></li>
<li><a href="https://www.everydev.ai/tools/torchtitan">torchtitan - PyTorch Native LLM Training Platform | EveryDev.ai</a></li>

</ul>
</details>

**Tags**: `#MoE`, `#TorchTitan`, `#distributed training`, `#PyTorch`, `#GH200`

---

<a id="item-tech-news-2"></a>
### [orcasairband.com live-transcribes airband radio from KORS with dual GPUs](https://orcasairband.com/) ⭐️ 7.0/10

A live airband monitoring site at orcasairband.com covers the full airband from Orcas Island \(KORS\), with its creator describing an Ettus B210 feeding a dual RTX 4090 machine that uses CUDA-based polyphase channelization to demodulate transmissions and generate raw transcripts. It drew attention during a ground stop affecting Vancouver traffic, when the feed captured exchanges about stopped traffic and a pilot confirming the ground stop. The creator says the transcripts are unedited, and commenters reported that many transmissions are heavily garbled.

hackernews · mmaunder · Nov 13, 22:04 · [Discussion](https://news.ycombinator.com/item?id=50490593)

**「Background」** VHF airband communications between controllers and pilots use analog AM voice on discrete channels spread across roughly 118–137 MHz, so a listener normally monitors one frequency at a time. A ground stop is an air traffic control instruction halting departures bound for a particular airport, and it is typically relayed to pilots over those same frequencies. The project&\#x27;s author describes capturing the whole band at once with an Ettus B210 receiver feeding a polyphase channelizer and demodulator written in CUDA and run on dual RTX 4090 GPUs.

**「Impact」** For nearby pilots and aviation listeners, the feed offers a near-real-time view of local airband chatter, but because the posted transcripts are raw and commenters found many transmissions hard to follow, it should be treated as a monitoring aid rather than a reliable operational source.

**「Community discussion」** The creator explains that the system uses an Ettus B210 and two RTX 4090 GPUs to channelize and demodulate the full airband before transcribing detected transmissions. Commenters highlighted timestamped transcripts from the ground stop, while one questioned why so many transmissions sound garbled and asked whether airband radio remains analog for security or interoperability.

**Tags**: `#software-defined radio`, `#CUDA signal processing`, `#airband communications`, `#real-time transcription`, `#GPU computing`

---

<a id="item-tech-news-3"></a>
### [FAA Issues Nationwide Ground Stop, Later Reported Lifted](https://www.nbcnews.com/news/us-news/faa-orders-nationwide-ground-stop-departing-flights-reasons-safety-rcna609247) ⭐️ 7.0/10

The FAA issued a nationwide ground stop on Nov. 13, 2026, halting departing flights across the U.S.; reports from NYT and CNBC cited in the discussion said it was later lifted. The item did not confirm the cause. WSJ reporting quoted in comments said the disruption appeared to affect an L3Harris Technologies telecommunications network that handles radio frequencies air-traffic controllers use to communicate with pilots. A commenter also speculated that the FAA’s recently announced AI air-traffic-control rollout was involved, but that link was unverified.

hackernews · zulln · Nov 13, 21:05 · [Discussion](https://news.ycombinator.com/item?id=50489641)

**「Background」** A ground stop is an emergency traffic-management measure that halts departures at affected airports while flights already airborne continue, used when a shared safety system cannot be trusted. The last comparable nationwide halt was in January 2023, when the FAA&\#x27;s NOTAM system failed; the current stoppage was attributed to a temporary telecommunications outage, a different system from the notice feed.

**「Operational impact」** The nationwide ground stop delayed or canceled more than 11,000 U.S. flights, and the FAA lifted the order about four hours after issuing it.

**「Community Discussion」** Commenters criticized how little official information was available, with one tracking LAX noting no departures after about 10:30 a.m. PST and another questioning whether the FAA’s newly announced AI air-traffic-control rollout was to blame; that AI link was speculation, not confirmed. Later comments cited NYT and CNBC reports that the ground stop had been lifted.

<details><summary>References</summary>
<ul>
<li><a href="https://www.alexjoneslive.com/2026/11/13/faa-issues-nationwide-ground-stop-due-to-extraordinary-circumstances/">FAA Issues Nationwide Ground Stop Due To... - Alex Jones Live</a></li>
<li><a href="https://www.theguardian.com/us-news/live/2026/nov/13/us-politics-latest-news-updates-democrats-republicans-donald-trump-van-hollen-chuck-schumer">US flight outage live updates: FAA grounds thousands... | The Guardian</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/faa-ground-stop.html">FAA lifts ground stop after four hours, but flight ... - CNBC</a></li>
<li><a href="https://www.theguardian.com/world/2026/nov/13/faa-nationwide-ground-stop-flights">Nationwide FAA ground stop: nearly 11,000 flights delayed or ...</a></li>

</ul>
</details>

**Tags**: `#FAA ground stop`, `#air traffic control`, `#critical infrastructure`, `#telecom outage`, `#AI in aviation`

---

<a id="item-tech-news-4"></a>
### [Haskell ecosystem technical vision sparks debate on tooling and AI](https://discourse.haskell.org/t/a-technical-vision-for-the-haskell-ecosystem/15078) ⭐️ 7.0/10

A community-written &quot;technical vision for the Haskell ecosystem&quot; was published on the Haskell Discourse and surfaced on Hacker News, framing a direction for the language&\#x27;s ecosystem rather than announcing a shipped release or dated roadmap commitment. The document&\#x27;s specific proposals are not included in the supplied material, so its concrete recommendations cannot be verified here. Reaction focused on adoption questions instead: whether Haskell&\#x27;s terseness and type safety suit AI-assisted code generation, why it lacks the cross-platform reach of JavaScript, Rust, and C\#, and whether build performance is the ecosystem&\#x27;s real bottleneck.

hackernews · cosmic\_quanta · Nov 13, 14:43 · [Discussion](https://news.ycombinator.com/item?id=50484235)

**「Who is behind the vision」** The post is the first public output of the Haskell Foundation&\#x27;s technical leadership committee, which the thread&\#x27;s opening message describes as having been bootstrapped over the preceding weeks of discussion and now &quot;fully operational.&quot; That makes it a statement of collective direction from the body set up to steer the ecosystem rather than one contributor&\#x27;s proposal — a secondary report on the committee&\#x27;s launch said it aimed to make GHC&\#x27;s checks roughly three times faster, though the supplied excerpt of the post itself does not give that figure.

**「Impact」** For Haskell tooling contributors, the response suggests the vision will be judged on build and debugging outcomes rather than language features: one commenter argued the priority should be incremental builds specifically, not compile time in general, while another pointed to live step-through debugging in a Haskell VR compositor as an area the ecosystem has underinvested in.

**「Community discussion」** Commenters split on where Haskell should aim: one argued its terseness and strictness make it a strong candidate for agentic AI code generation, while another said the language&\#x27;s real weakness is that it is not universal like C, C++, JavaScript, Rust, or C\# for desktop, mobile, and web work. A third reported positive recent experience building a STEP file reader/writer in Haskell that came within 20-30% of C performance on the largest CAD assemblies tested, and credited hasufell for clear-headed input on ecosystem direction.

<details><summary>References</summary>
<ul>
<li><a href="https://discourse.haskell.org/t/a-technical-vision-for-the-haskell-ecosystem/15078">A technical vision for the Haskell ecosystem - Haskell Foundation...</a></li>
<li><a href="https://dzen.ru/b/avdWQF0woA1Z8MqS">Haskell Foundation запустила техкомитет: цель — ускорить... | Дзен</a></li>

</ul>
</details>

**Tags**: `#Haskell`, `#programming languages`, `#ecosystem strategy`, `#developer tooling`, `#open source`

---

<a id="item-tech-news-5"></a>
### [Python early contributor Tim Peters dies at 74](https://x.com/Itsfoss/status/2120957452937998716) ⭐️ 7.0/10

Tim Peters, an early Python contributor known for the Timsort sorting algorithm and PEP 20, “The Zen of Python,” has died at age 74, according to a Telegram post relaying a statement attributed to Python creator Guido van Rossum. The item says Peters was Python’s second real user and served 13 years on the Python Software Foundation board. The report is an aggregation of a social-media post and does not include independent confirmation or a cause of death.

telegram · zaihuapd · Nov 13, 09:55

**「Background」** Peters posted the principles that became PEP 20, The Zen of Python, to the Python mailing list in 1999, leaving an open 20th principle for Guido van Rossum to fill in. Python users know the text as the output of \`import this\`.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Zen_of_Python">Zen of Python - Wikipedia</a></li>
<li><a href="https://news.ycombinator.com/item?id=50450488">Tim Peters has died | Hacker News</a></li>

</ul>
</details>

**Tags**: `#Python`, `#open source`, `#software community`, `#obituary`, `#Tim Peters`

---

<a id="item-tech-news-6"></a>
### [Microsoft 365 outage hits Outlook, Teams and Copilot worldwide](https://www.reuters.com/technology/microsoft-365-outlook-down-thousands-us-users-downdetector-shows-2026-11-12/) ⭐️ 7.0/10

Microsoft&\#x27;s Outlook, Teams and Copilot services remained down on Nov. 13 in an outage lasting more than 12 hours, disrupting enterprise and government communications worldwide. Microsoft attributed the failure to a server issue, said it found no evidence of malicious activity, and reported that it had expanded remediation and was seeing signs of recovery. Government agencies in Australia, Japan and parts of the U.S. were affected, Euronext email was disrupted, and some Taiwanese financial institutions switched to fax to confirm trades, according to the report. The report described it as Microsoft 365&\#x27;s second service disruption this year.

telegram · zaihuapd · Nov 13, 12:21

**「Background」** Microsoft 365 is the cloud suite through which Microsoft delivers Outlook, Teams and Copilot, so a platform-level server fault can affect several of those services at once. The source notes that this was the second Microsoft 365 disruption this year, after an earlier outage that it does not describe in detail.

**「Impact」** Affected organizations had to fall back on alternate channels: some Taiwanese financial institutions confirmed trades by fax, and Euronext&\#x27;s email was disrupted, illustrating the need for tested out-of-band procedures when Outlook and Teams are unavailable for time-sensitive operations.

**Tags**: `#Microsoft 365`, `#cloud outage`, `#reliability`, `#enterprise software`, `#Copilot`

---

<a id="item-tech-news-7"></a>
### [DeepSeek opens app API for search, files, and voice](https://mp.weixin.qq.com/s/78KBHc4-4N5b2vfL9SkutQ) ⭐️ 7.0/10

DeepSeek has opened a set of application APIs that let developers enable conversational capabilities—deep-thinking search, file input, link reading, and voice—through parameters in the existing API, with the server handling tool calls and context stitching. The V4.1-Flash model is supported across three interfaces, while Search, Fetch, OCR, ASR, and TTS can also be called separately. DeepSeek also open-sourced a chat frontend demo that can import conversation history and, using the API, run a local deployment of the DeepSeek web interface.

telegram · zaihuapd · Nov 13, 14:27

**「Background」** DeepSeek&\#x27;s existing API exposed model inference directly, so applications that needed search, file handling, or speech had to integrate those services separately. The new capability set shifts that work to the server side: developers turn on parameters in their existing API calls, and DeepSeek performs the tool invocation and context assembly itself, while the individual Search, Fetch, OCR, ASR, and TTS services remain separately callable.

**「Developer impact」** Developers building on DeepSeek&\#x27;s API can now enable search, file input, link reading, OCR, ASR and TTS through existing endpoints, with the server handling tool orchestration and context assembly, and can also call those services standalone for custom pipelines. The documented built-in support is limited to V4.1-Flash across three interfaces, so teams using other models should confirm availability before depending on the parameter-based path; the open-source chat demo provides a deployable frontend reference.

<details><summary>References</summary>
<ul>
<li><a href="https://api-docs.deepseek.com/news/news261113/">The full DeepSeek App experience, now via API | DeepSeek API Docs</a></li>

</ul>
</details>

**Tags**: `#DeepSeek`, `#AI APIs`, `#multimodal`, `#tool calling`, `#open source`

---

<a id="item-tech-news-8"></a>
### [OpenAI launches ChatGPT Wallet for agent payments with Visa, Mastercard, Amex](https://openai.com/index/introducing-chatgpt-wallet/) ⭐️ 7.0/10

OpenAI announced ChatGPT Wallet, a payment wallet that lets ChatGPT agents make purchases without handling users&\#x27; real card numbers, in partnership with American Express, Mastercard and Visa. According to the announcement, payment networks issue a token that substitutes for the actual card number, and each transaction requires the user to review the item and amount and confirm with Face ID or fingerprint. Access starts today in the US for ChatGPT Pro subscribers aged 18 and over with a US-issued card, distributed through a reference in the post to &quot;dots&quot; whose meaning cannot be verified from the supplied material. The source is a short aggregator post with no architecture detail, pricing, transaction limits or independent confirmation of the capability, so the rollout&\#x27;s actual scope is not established.

telegram · zaihuapd · Nov 13, 15:43

**「Background」** ChatGPT Wallet is tied to OpenAI&\#x27;s &quot;dots&quot; agents, which act on a user&\#x27;s behalf and can complete purchases through the wallet. It builds on card-network tokenization: the payment networks issue a substitute credential linked to an existing card, so an agent can transact without receiving the underlying card number.

**「What It Means for Users」** Eligibility is narrow: only ChatGPT Pro subscribers aged 18+ with a US-issued card can use the wallet at launch, so other users and non-US cards are excluded for now. Every purchase also requires the user to review the item and amount and approve it with Face ID or a fingerprint, which means agents can prepare and check out orders but cannot complete unattended or background purchases without that per-transaction confirmation.

<details><summary>References</summary>
<ul>
<li><a href="https://tech.yahoo.com/ai/chatgpt/articles/openai-introduces-chatgpt-wallet-visa-162102250.html">OpenAI Introduces ChatGPT Wallet With Visa, Mastercard, Amex ...</a></li>
<li><a href="https://cointelegraph.com/news/openai-ai-payments-chatgpt-wallet-visa-mastercard-amex">OpenAI Launches ChatGPT Wallet for AI Agent Payments</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/openai-chatgpt-wallet-dot-purchases.html">OpenAI&#x27;s ChatGPT Wallet allows &#x27;dots&#x27; AI agents to make purchases</a></li>
<li><a href="https://www.reuters.com/technology/openai-launches-chatgpt-wallet-letting-ai-agents-pay-purchases-2026-11-13/">OpenAI launches ChatGPT Wallet, letting AI agents pay for ...</a></li>

</ul>
</details>

**Tags**: `#openai`, `#ai-agents`, `#agentic-commerce`, `#payments`, `#fintech`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Cantor Fitzgerald trimmed its reported Nvidia stake as Washington scrutinized the chipmaker](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 8.0/10

Cantor Fitzgerald, the Wall Street firm now led by Commerce Secretary Howard Lutnick&\#x27;s sons, reported a 49% drop in the number of Nvidia shares it held between September 2025 and March 2026 — to 1.78 million shares worth $310 million, from 3.5 million worth $652 million — while continuing to arrange billions of dollars in financing for the chipmaker&\#x27;s business partners, CNBC reported, drawing conflict-of-interest questions as officials scrutinize suspected Nvidia chip smuggling to China. Cantor said its Nvidia positions were &quot;immaterial&quot; proprietary holdings tied to ordinary client swap transactions, and CNBC said it found no evidence that the holdings changed because of intelligence warnings or that the firm&\#x27;s business interests influenced Lutnick&\#x27;s decisions.

rss · CNBC Finance · Nov 13, 23:42

**「Background」** Howard Lutnick ran Cantor Fitzgerald until he became commerce secretary in February 2025, and the department he now leads administers U.S. export controls, including the entity list that restricts which foreign companies may buy American technology.

**「Impact」** The dispute has direct stakes for Nvidia&\#x27;s distributors and cloud partners, because entity-list designations for firms suspected of diverting its chips to China are decided by Commerce — and Cantor has helped arrange financing for at least one such partner, IREN.

**Tags**: `#Nvidia`, `#Howard Lutnick`, `#Cantor Fitzgerald`, `#China export controls`, `#conflict of interest`

---

<a id="item-finance-news-2"></a>
### [Goolsbee Says Fed Has &\#x27;Work to Do&\#x27; on Inflation After PPI Rise](https://www.cnbc.com/2026/11/13/chicago-feds-goolsbee-says-central-bank-has-definitely-got-work-to-do-on-inflation.html) ⭐️ 7.0/10

Chicago Fed President Austan Goolsbee said the central bank &quot;has definitely got work to do&quot; to restore credibility on inflation, after the producer price index rose 0.3% in October and 6.5% from a year earlier—the highest annual gain since November 2022. Markets are fully pricing a quarter-point rate increase at the Dec. 8-9 FOMC meeting, according to CME Group&\#x27;s FedWatch.

rss · CNBC Finance · Nov 13, 14:22

**「Background」** The PPI is a gauge of wholesale prices, and the Fed targets 2% annual inflation; Goolsbee is not an FOMC voter until 2027.

**Tags**: `#Federal Reserve`, `#inflation`, `#producer price index`, `#monetary policy`, `#interest rates`

---

<a id="item-finance-news-3"></a>
### [Jensen Huang resigns from Nvidia; analysts see tighter China export controls](https://www.cnbc.com/2026/11/13/jensen-huang-nvidia-us-china-relations.html) ⭐️ 7.0/10

Former Nvidia CEO Jensen Huang resigned Thursday and agreed to testify before Congress by Nov. 26 over an affair with a woman U.S. intelligence sources allege was a Chinese spy. Analysts cited by CNBC predict the scandal could prompt Congress to tighten U.S. export controls on China before year-end.

rss · CNBC Finance · Nov 13, 02:56

**「Background」** The case lands on a fragile U.S.-China trade truce; Washington began restricting Nvidia’s advanced chip sales to China in 2022, and the Trump administration eased many Biden-era limits in 2025, while Huang had argued U.S. technology needed to remain in China to stay globally relevant.

**「Impact」** Analysts warn that tighter U.S. export rules would affect Chinese buyers of advanced chips and U.S. semiconductor suppliers, and Beijing could retaliate by restricting rare-earth or chipmaking-material supplies.

**Tags**: `#Nvidia`, `#Jensen Huang`, `#US-China relations`, `#export controls`, `#semiconductors`

---