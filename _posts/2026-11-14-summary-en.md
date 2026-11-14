---
layout: default
title: "Horizon Summary: 2026-11-14 (EN)"
date: 2026-11-14
lang: en
---

> From 39 items, 10 important content pieces were selected

---

**Technology News**
1. [TorchTitan trains 1T-parameter MoE on 384 GH200 GPUs at ~1,300 tokens/s per GPU](#item-tech-news-1) ⭐️ 8.0/10
2. [Shanghai Jiao Tong gene-editing case found lacking ethics and consent](#item-tech-news-2) ⭐️ 8.0/10
3. [FAA orders nationwide ground stop for departing flights](#item-tech-news-3) ⭐️ 7.0/10
4. [ICML 2027 reportedly adds submission caps and two-stage review](#item-tech-news-4) ⭐️ 7.0/10
5. [Microsoft Outlook, Teams and Copilot global outage exceeds 12 hours](#item-tech-news-5) ⭐️ 7.0/10
6. [DeepSeek Opens App APIs for Search, Files, Voice, Tool Calling](#item-tech-news-6) ⭐️ 7.0/10
7. [OpenAI launches ChatGPT Wallet for agent payments with card-network tokens](#item-tech-news-7) ⭐️ 7.0/10

**Financial News**
1. [Lutnick faces scrutiny over Cantor Fitzgerald’s Nvidia ties](#item-finance-news-1) ⭐️ 8.0/10
2. [Chicago Fed&\#x27;s Goolsbee says the Fed &\#x27;has definitely got work to do&\#x27; on inflation](#item-finance-news-2) ⭐️ 7.0/10
3. [Nvidia&\#x27;s Jensen Huang resigns amid spy-allegation scrutiny](#item-finance-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [TorchTitan trains 1T-parameter MoE on 384 GH200 GPUs at ~1,300 tokens/s per GPU](https://www.reddit.com/r/MachineLearning/comments/1xvce5h/scaling_to_1t_moe_on_torchtitan_p/) ⭐️ 8.0/10

A team working with TorchTitan and PyTorch maintainers reports training a ~1T-parameter mixture-of-experts model on 384 GH200 GPUs — the hardware inside the JUPITER supercomputer — at roughly 1,300 tokens/s per GPU, which they describe as 14x their starting point. The setup used 384-way FSDP plus 4-way expert parallelism kept strictly inside each node, and skipped pipeline parallelism to avoid long steps. Their baseline step took 84 seconds, 68 of which were spent waiting on InfiniBand at ~25 GB/s per GPU. Reported gains include full activation checkpointing \(4x\), offloading checkpoint activations to Grace over the 900 GB/s C2C link, Muon instead of Adam to reach 64k-token sequences, and running Newton-Schulz on the GPU while optimizer state stays on the host, which cut the optimizer step from 42 s to ~2 s \(+35%\). The post also reports cost-bucketed sequence packing \(+13%, worst rank from 7.9x to 1.15x the average\), a bf16 expert-gradient all-to-all replacing the fp32 reduce-scatter, and FP8 expert all-gather with blockwise scales \(+18%\); these are the authors&\#x27; own measurements, with full plots on the Domyn and PyTorch blogs rather than an independent benchmark.

reddit · r/MachineLearning · /u/f14-bertolotti · Nov 13, 16:28

**「Context」** TorchTitan is PyTorch&\#x27;s reference stack for large-scale distributed pretraining, and GH200 pairs a Hopper GPU with a Grace CPU over a 900 GB/s cache-coherent link, which is what let the team treat host memory as storage for activations and optimizer state. FSDP shards every parameter across ranks and re-gathers each layer just in time, while expert parallelism assigns whole experts to specific ranks so tokens must be routed to them over the network.

**「What it means for practitioners」** Two of the fixes are contributions rather than local hacks: Newton-Schulz on the GPU with host-resident parameters, and the FSDP2 \`unshard\_async\_op\` flag \(currently private\) that moves collective temporaries onto the compute stream, which the post says is on its way to becoming public API. Their caching-allocator diagnosis is a directly actionable one for anyone seeing allocator retries at ~70% HBM utilization with tens of GiB still cached. The authors flag group-limited routing as the one win with a caveat: it gave +7% by making expert load perfectly even, but early runs suggest constraining where the router may send tokens can hurt training quality.

**Tags**: `#distributed training`, `#Mixture-of-Experts`, `#PyTorch`, `#GPU scaling`, `#large language models`

---

<a id="item-tech-news-2"></a>
### [Shanghai Jiao Tong gene-editing case found lacking ethics and consent](https://mp.weixin.qq.com/s/p0iC3tcI1yr10EBl2NjUvg) ⭐️ 8.0/10

Shanghai&\#x27;s investigation into a customized gene-editing therapy at Shanghai Jiao Tong University School of Medicine found deficiencies in preclinical research, ethics review, and informed consent, and said some personnel received about 1.06 million yuan in money or property from the patient&\#x27;s family. The patient, a child with Snijders Blok-Campeau syndrome, died in March 2025 from thrombotic microangiopathy after the injection; the case paper was published in Nature in February 2026. The researcher identified as Qiu and another identified as Yang were dismissed and disqualified for five years, while the involved institutions were ordered to rectify and received administrative penalties. The post attributes the findings to Xinhua; the underlying investigation documents were not independently reviewed here.

telegram · zaihuapd · Nov 13, 09:24

**「Background」** Snijders Blok-Campeau syndrome is a rare disease, and the therapy at issue was custom-developed for one affected child after the family approached the research team in 2023, rather than tested through a standard multi-patient trial. That single-patient setting makes preclinical safety data, independent ethics review, and informed consent the central safeguards—the same areas Shanghai&\#x27;s investigation found deficient after the child died from thrombotic microangiopathy following a March 2025 injection.

**「Impact」** The penalties extend beyond the two named researchers to the institutions, which were ordered to rectify and faced administrative penalties—showing that ethics-review and consent failures in customized gene-editing work can trigger organizational sanctions, not just individual discipline.

**Tags**: `#gene editing`, `#research ethics`, `#clinical trials`, `#biotech regulation`, `#scientific misconduct`

---

<a id="item-tech-news-3"></a>
### [FAA orders nationwide ground stop for departing flights](https://www.nbcnews.com/news/us-news/faa-orders-nationwide-ground-stop-departing-flights-reasons-safety-rcna609247) ⭐️ 7.0/10

The FAA issued a nationwide ground stop for departing flights on Nov. 13, 2026, according to NBC News, temporarily halting departures across U.S. airports. The supplied material does not confirm the cause; commenters cited a WSJ report that an L3Harris Technologies telecommunications network carrying air-traffic-control radio frequencies was affected, but that account was not independently verified. Commenters also raised unverified speculation about a recent AI-ATC rollout, and reports on whether the stop had been lifted conflicted.

hackernews · zulln · Nov 13, 21:05 · [Discussion](https://news.ycombinator.com/item?id=50489641)

**「What preceded the stop」** The stoppage traces to a communications failure: reporting citing people briefed on the matter says the affected system is a telecommunications network overseen by L3Harris Technologies that carries the radio frequencies controllers use to talk with pilots. The outage also arrived days after the FAA said it would expand SMART, an $875 million AI route-management tool, to assist with traffic across the entire national airspace — an expansion some commenters linked to the stoppage without evidence. The FAA has stated that SMART advises on congestion and &quot;cannot be used to replace the critical role air traffic controllers play or take over control of an aircraft.&quot;

**「Impact」** Although the ground stop was lifted after about four hours, it had already disrupted thousands of departing flights, leaving airlines and travelers to manage cascading cancellations and delays as operations resume. Officials initially had no timeline for resolving the telecommunications issue behind the stop.

**「Community discussion」** Commenters focused on the cause, citing a WSJ report that an L3Harris-run network for controller-pilot radio communications was affected and speculating without confirmation that a recently announced AI-ATC rollout was responsible. They also reported airport departure boards stalled or showing delays and offered conflicting accounts of whether the ground stop had been lifted.

<details><summary>References</summary>
<ul>
<li><a href="https://www.theguardian.com/us-news/live/2026/nov/13/us-politics-latest-news-updates-democrats-republicans-donald-trump-van-hollen-chuck-schumer">US flight outage live updates: FAA grounds thousands... | The Guardian</a></li>
<li><a href="https://arstechnica.com/ai/2026/11/faa-expands-ai-advice-to-manage-air-traffic-congestion-across-entire-us-airspace/">FAA expands AI advice to manage air traffic ... - Ars Technica</a></li>
<li><a href="https://gizmodo.com/the-faa-is-rolling-out-its-ai-air-traffic-tool-nationwide-2000839347">The FAA Is Rolling Out Its AI Air Traffic Tool Nationwide</a></li>
<li><a href="https://www.cnn.com/2026/11/13/us/live-news/flights-ground-stop-faa">Live updates on FAA ground stop : No timeline for resolution as flight ...</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/faa-ground-stop.html">FAA lifts ground stop after four hours, but flight cancellations will...</a></li>

</ul>
</details>

**Tags**: `#FAA ground stop`, `#critical infrastructure`, `#air traffic control`, `#telecommunications outage`, `#AI-ATC speculation`

---

<a id="item-tech-news-4"></a>
### [ICML 2027 reportedly adds submission caps and two-stage review](https://www.reddit.com/r/MachineLearning/comments/1xvkxbj/icml_2027_changes_d/) ⭐️ 7.0/10

A Reddit post summarizing what it describes as ICML 2027&\#x27;s call for papers reports a two-stage review process: an area chair decides whether a paper proceeds to full review, any first-stage rejection must be confirmed by a senior area chair, and authors receive a short justification by Feb. 23. The reported rules also cap involvement at 20 submissions per person, require every paper to name a reciprocal reviewer from its author list \(max six papers per reviewer\), require program-committee service for anyone with three or more submissions, and warn that noncompliant papers may be desk rejected. Each author would also be limited to at most one paper with no eligible reciprocal reviewer among its authors.

reddit · r/MachineLearning · /u/Gravitist · Nov 13, 21:53

**「Why ICML is changing review rules」** ICML&\#x27;s call for papers sets the submission and reviewing obligations that authors and program-committee members must meet. The poster describes the 2027 rules as a response to years of submission growth and reviewer overload at ML conferences, with authorship volume now tied to reviewing duty. This item is a Reddit summary of the CFP, not an official ICML announcement.

**「Practical impact」** Under the reported policy, labs or collaborations planning multiple ICML 2027 submissions will need to allocate reviewer capacity up front: every paper must name an eligible reciprocal reviewer from its author list, each reviewer can cover at most six papers, and any author with three or more submissions must serve on the program committee. Because noncompliant papers may be desk-rejected, author lists and reviewer commitments should be settled before submission rather than after review decisions.

**Tags**: `#ICML`, `#peer review`, `#ML research`, `#conference policy`, `#submission limits`

---

<a id="item-tech-news-5"></a>
### [Microsoft Outlook, Teams and Copilot global outage exceeds 12 hours](https://www.reuters.com/technology/microsoft-365-outlook-down-thousands-us-users-downdetector-shows-2026-11-12/) ⭐️ 7.0/10

Microsoft&\#x27;s Outlook, Teams and Copilot services remained down on Nov. 13 in a global outage lasting more than 12 hours, disrupting enterprise and government communications. Microsoft attributed the cause to a server issue, said it found no malicious activity, and reported expanding remediation with signs of stabilization. Some government agencies in Australia, Japan and the United States were affected, Euronext&\#x27;s email was disrupted, and financial institutions in Taiwan used fax to confirm trades; the report described it as Microsoft 365&\#x27;s second outage this year.

telegram · zaihuapd · Nov 13, 12:21

**「Background」** Microsoft 365 has already experienced one other outage this year, according to the source. Microsoft attributed the disruption to server problems and said it found no sign of malicious activity. The Guardian reported that the outage also affected connectors used by OpenAI&\#x27;s and Anthropic&\#x27;s AI services, a reminder of how many third-party tools rely on Microsoft&\#x27;s cloud.

**「Impact」** For organizations that rely on Microsoft 365 for critical communications, the incident required fallback procedures: Taiwanese financial institutions used fax to confirm trades after normal channels failed. That makes tested out-of-band confirmation channels a concrete continuity requirement for affected financial and government users.

<details><summary>References</summary>
<ul>
<li><a href="https://www.theguardian.com/technology/2026/nov/13/microsoft-outage-outlook-teams-word-excel-reports">Microsoft scrambles to fix global outage affecting Teams and Outlook</a></li>

</ul>
</details>

**Tags**: `#Microsoft 365`, `#outage`, `#cloud reliability`, `#enterprise software`, `#incident response`

---

<a id="item-tech-news-6"></a>
### [DeepSeek Opens App APIs for Search, Files, Voice, Tool Calling](https://mp.weixin.qq.com/s/78KBHc4-4N5b2vfL9SkutQ) ⭐️ 7.0/10

DeepSeek announced application APIs that let developers enable parameters in the existing API to add deep-thinking search, file input, link reading, and voice to conversations, with server-side tool invocation and context assembly handled automatically. The V4.1-Flash model is supported in three interfaces, while Search, Fetch, OCR, ASR, and TTS can also be called individually. DeepSeek also released an open-source chat-demo front end that can import prior conversations and be deployed locally, according to the Telegram relay; the post gives no pricing, rate limits, endpoint details, or independent test results.

telegram · zaihuapd · Nov 13, 14:27

**「Background」** DeepSeek already offered model API access and a consumer app that handled search, file and link reading, and voice around the model. The new application API exposes that surrounding layer; DeepSeek&\#x27;s documentation says built-in features can be enabled with parameters or called as standalone OCR, ASR, and TTS services.

**「Impact」** For developers, the practical change is that one API can orchestrate search, fetching, OCR, ASR, and TTS server-side rather than requiring separate client-side integrations. However, the supplied relay does not list endpoint names, pricing, rate limits, or compatibility details, so production adoption requires checking DeepSeek&\#x27;s documentation and testing the new parameters.

<details><summary>References</summary>
<ul>
<li><a href="https://api-docs.deepseek.com/news/news261113/">The full DeepSeek App experience, now via API | DeepSeek API Docs</a></li>

</ul>
</details>

**Tags**: `#DeepSeek`, `#AI APIs`, `#multimodal AI`, `#tool calling`, `#open-source demo`

---

<a id="item-tech-news-7"></a>
### [OpenAI launches ChatGPT Wallet for agent payments with card-network tokens](https://openai.com/index/introducing-chatgpt-wallet/) ⭐️ 7.0/10

OpenAI has launched ChatGPT Wallet in partnership with American Express, Mastercard, and Visa, enabling AI agents to make purchases without accessing users&\#x27; real card numbers and requiring security verification for each purchase. Starting today, the wallet is available in the US through dots to ChatGPT Pro subscribers aged 18 and older who use a US-issued card. Users review the item and amount for each transaction and confirm with Face ID or a fingerprint, while the payment networks issue a token that replaces the real card number.

telegram · zaihuapd · Nov 13, 15:43

**「Background」** ChatGPT Wallet is built around card-network tokenization: the payment network issues a token in place of the real card number, so the purchasing agent never handles the underlying credentials. OpenAI developed it with American Express, Mastercard and Visa and is initially offering it through dots, its AI agents that can make purchases for users, to ChatGPT Pro subscribers in the US. The per-purchase check—reviewing the item and amount, then approving with Face ID or a fingerprint—is the control that replaces handing a card to an agent.

**「Impact」** Eligible users must have a ChatGPT Pro subscription and a US-issued card, and every agent purchase remains gated by item-and-amount review plus biometric confirmation, so the flow is not fully unattended checkout.

<details><summary>References</summary>
<ul>
<li><a href="https://openai.com/index/introducing-chatgpt-wallet/">Introducing ChatGPT Wallet | OpenAI</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/openai-chatgpt-wallet-dot-purchases.html">OpenAI &#x27;s ChatGPT Wallet allows &#x27;dots&#x27; AI agents to make purchases</a></li>

</ul>
</details>

**Tags**: `#OpenAI`, `#AI agents`, `#payments`, `#fintech`, `#security`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Lutnick faces scrutiny over Cantor Fitzgerald’s Nvidia ties](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 8.0/10

CNBC reported that Cantor Fitzgerald, the Wall Street firm formerly led by Commerce Secretary Howard Lutnick and now run by his sons, reported a nearly 50% decline in its Nvidia share count—from more than 3.5 million shares in September 2025 to 1.78 million by March 2026—as Lutnick faced scrutiny over Axios reports that he resisted a crackdown on suspected Nvidia chip smuggling to China. Nvidia CEO Jensen Huang resigned Thursday, and Cantor said its own Nvidia positions were not significant and that its filing positions reflected client transactions; CNBC said there is no evidence the share decline was tied to intelligence warnings or influenced Lutnick’s decisions.

rss · CNBC Finance · Nov 13, 23:42

**「Background」** Washington has restricted exports of Nvidia&\#x27;s most advanced AI chips to China since 2022, and the Commerce Department — run by Howard Lutnick, formerly Cantor Fitzgerald&\#x27;s chief executive, since February 2025 — is the agency that enforces those controls. Nvidia CEO Jensen Huang resigned on Thursday after reports that he had extramarital relationships, including one with a suspected agent of China, which brought fresh scrutiny to Lutnick&\#x27;s and his family&\#x27;s financial ties to the chipmaker.

<details><summary>References</summary>
<ul>
<li><a href="https://www.bbc.com/news/articles/c67429m3vem3o">How a sex scandal at Nvidia is putting pressure on the White House</a></li>
<li><a href="https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html">Howard Lutnick’s sons’ Nvidia ties amid Jensen Huang China spy ...</a></li>
<li><a href="https://www.nbcnews.com/tech/tech-news/nvidia-ceo-jensen-huang-resigns-reports-extramarital-relationships-rcna608402">Nvidia CEO Jensen Huang resigns after reports of affair and...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#Howard Lutnick`, `#Cantor Fitzgerald`, `#US-China export controls`, `#conflict of interest`

---

<a id="item-finance-news-2"></a>
### [Chicago Fed&\#x27;s Goolsbee says the Fed &\#x27;has definitely got work to do&\#x27; on inflation](https://www.cnbc.com/2026/11/13/chicago-feds-goolsbee-says-central-bank-has-definitely-got-work-to-do-on-inflation.html) ⭐️ 7.0/10

Chicago Fed President Austan Goolsbee said the central bank &quot;has definitely got work to do to continue to reestablish its credibility&quot; on inflation, after the producer price index rose 6.5% over the year to October — the highest annual reading since November 2022. Markets are fully pricing a quarter-point rate increase at the Federal Open Market Committee&\#x27;s Dec. 8-9 meeting, with a better than 10% probability of a half-point move, according to CME Group&\#x27;s FedWatch futures gauge.

rss · CNBC Finance · Nov 13, 14:22

**「Background」** The Fed targets 2% inflation, and Goolsbee said price growth has been above that level for almost six years and recently stopped improving, pointing to AI data-center demand as an added source of price pressure; he is not currently an FOMC voter.

**「Impact」** If the Fed raises rates as markets expect, households and businesses taking out new or variable-rate loans would face higher borrowing costs.

**Tags**: `#Federal Reserve`, `#inflation`, `#PPI`, `#interest rates`, `#monetary policy`

---

<a id="item-finance-news-3"></a>
### [Nvidia&\#x27;s Jensen Huang resigns amid spy-allegation scrutiny](https://www.cnbc.com/2026/11/13/jensen-huang-nvidia-us-china-relations.html) ⭐️ 7.0/10

Former Nvidia CEO Jensen Huang resigned Thursday and agreed to testify before Congress before Nov. 26 amid scrutiny of an affair with a woman reported to be an alleged Chinese spy. Analysts say the controversy could harden U.S. chip export controls and complicate the fragile U.S.-China trade truce.

rss · CNBC Finance · Nov 13, 02:56

**「Background」** Washington has restricted Nvidia&\#x27;s sales of advanced chips to China since 2022, though the Trump administration eased many Biden-era limits in 2025; Huang had argued that U.S. technology must be used in China to remain globally relevant.

**「Impact」** Analysts warn Nvidia could face tighter U.S. export rules before year-end, while Beijing may curb rare-earth or chipmaking-materials supplies and accelerate its push for domestic alternatives.

**Tags**: `#US-China relations`, `#Nvidia`, `#semiconductor export controls`, `#Congressional scrutiny`, `#AI competition`

---