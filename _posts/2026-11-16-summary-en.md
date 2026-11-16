---
layout: default
title: "Horizon Summary: 2026-11-16 (EN)"
date: 2026-11-16
lang: en
---

> From 36 items, 8 important content pieces were selected

---

**Technology News**
1. [Meta FAIR/NYU: MLLM vision pretraining optional, dedicated vision parameters required](#item-tech-news-1) ⭐️ 8.0/10
2. [Meituan releases LongCat-2.5 weights, claims Huawei Ascend-only training](#item-tech-news-2) ⭐️ 8.0/10
3. [MacBook Pro OLED PWM flicker sparks sensitivity and frequency debate](#item-tech-news-3) ⭐️ 7.0/10
4. [Protomaps PMTiles: cheap self-hosted map tiles for projects](#item-tech-news-4) ⭐️ 7.0/10
5. [Sebastian Raschka Explains Positional Embeddings in Modern LLMs](#item-tech-news-5) ⭐️ 7.0/10

**Financial News**
1. [Cantor Fitzgerald cut Nvidia stake amid Lutnick ethics scrutiny](#item-finance-news-1) ⭐️ 8.0/10
2. [U.S. Judge Rejects Dismissal of DRAM Price-Fixing Lawsuit Against Micron, Samsung and SK Hynix](#item-finance-news-2) ⭐️ 7.0/10
3. [China, US and Russia to Hold First Trilateral Leaders’ Meeting at Shenzhen APEC](#item-finance-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Meta FAIR/NYU: MLLM vision pretraining optional, dedicated vision parameters required](https://www.reddit.com/r/MachineLearning/comments/1xx1k2o/meta_fair_nyu_unbundling_multimodal_vision/) ⭐️ 8.0/10

A Meta FAIR and NYU team reports training more than 200 multimodal LLMs from scratch on the same data—charging encoder pretraining to the same compute budget—to separate encoder pretraining, vision-only parameters, and encoder placement. Across 16 VQA benchmarks at 448 px and 12 language benchmarks, separately pretrained encoders at best tied from-scratch encoders at matched compute in Qwen3-1.7B/4B configurations with 0.4B vision parameters; pretraining MetaCLIP 6.5× longer lifted ImageNet linear-probe accuracy from 80.4% to 84.4% without improving VQA. Encoder-free models trailed from 0.6B to 6.4B and needed about 3× the compute to catch up, whereas an “in-fusion” design adding zero-initialized vision-only weights to the LLM&\#x27;s first eight layers matched the encoder from 1.7B to 6.4B with about 13% lower time to first token \(45.0 vs 44.4 VQA at 1.7B\).

reddit · r/MachineLearning · /u/trungh98 · Nov 15, 17:38

**「Background」** Most multimodal LLMs conventionally bundle three things into one vision encoder: separate pretraining \(typically CLIP-style contrastive or captioning objectives\), parameters used only by vision tokens, and placement ahead of the language model. Recent published recipes diverge — some train the encoder from scratch alongside the LLM, others remove it entirely — but comparing those models cannot isolate the encoder&\#x27;s contribution, since they differ in training data and compute and rarely account for pretraining cost. The Meta FAIR and NYU study separates the bundled encoder into those three design choices and tests each one independently under matched compute, with every model trained from scratch.

**「Impact」** For MLLM developers, the reported result argues against spending scarce pretraining compute on a separate vision encoder under a matched budget, but it does not support removing dedicated vision capacity: encoder-free models needed about 3× the compute in this setup. Teams optimizing latency may test in-fusion placement, while treating the finding as specific to the paper&\#x27;s data, 0.4B vision capacity, and 448 px evaluation.

<details><summary>References</summary>
<ul>
<li><a href="https://arxiv.org/pdf/2611.17334v1">Unbundling Multimodal Vision Encoding - arXiv.org</a></li>
<li><a href="https://sparsenotes.com/posts/2026/11/papers/unbundling-multimodal-vision-encoding/">Unbundling Multimodal Vision Encoding | Sparse Notes</a></li>

</ul>
</details>

**Tags**: `#multimodal LLMs`, `#vision encoders`, `#model architecture`, `#pretraining`, `#research`

---

<a id="item-tech-news-2"></a>
### [Meituan releases LongCat-2.5 weights, claims Huawei Ascend-only training](https://the-decoder.com/meituan-releases-a-1-6-trillion-parameter-agent-model-that-never-touched-an-nvidia-gpu/) ⭐️ 8.0/10

Meituan&\#x27;s LongCat team has released the open weights for LongCat-2.5, a 1.6-trillion-parameter multimodal agent model with about 48 billion parameters activated per token, under an MIT license that permits commercial use. The model accepts text, image, and video input and is aimed at agents that autonomously carry out long, multi-step tasks, especially coding. Meituan claims the model was trained entirely on Huawei Ascend accelerators without Nvidia GPUs, and reports an 88.4 score on Terminal Bench v2.1 versus 89.1 for Claude Opus 5. The training claim and the single benchmark result are vendor-reported and have not been independently verified.

telegram · zaihuapd · Nov 15, 11:08

**「Earlier LongCat release」** LongCat-2.5 follows Meituan&\#x27;s LongCat-2.0, which the company described as trained and served end-to-end on Huawei Ascend chips with no Nvidia hardware and released under an MIT license. Coverage of that earlier release also reported that Huawei Ascend, MetaX, and Muxi announced inference compatibility shortly after the weights appeared, making domestic-chip deployment part of the LongCat line&\#x27;s stated positioning rather than a claim introduced only with 2.5.

**「Impact」** Developers can commercially use an MIT-licensed agent model that handles text, image, and video input, which matters for teams building multimodal autonomous workflows. The reported 88.4 Terminal Bench v2.1 score is close to Claude Opus 5&\#x27;s 89.1 but is a single vendor-reported result, so teams evaluating it should benchmark it on their own coding tasks.

<details><summary>References</summary>
<ul>
<li><a href="https://aicodingweekly.datadriftpress.com/p/61-longcat-edges-out-gpt-5-5">#61 - LongCat edges out GPT-5.5 | AI Coding Weekly</a></li>
<li><a href="https://www.ainchina.com/blog/meituan-longcat-2-trillion-domestic-chips-china-ai-independence-2026/">How Meituan Built a Trillion - Parameter AI Model on 50,000 Domestic...</a></li>

</ul>
</details>

**Tags**: `#large language models`, `#open weights`, `#agentic coding`, `#Huawei Ascend`, `#AI hardware`

---

<a id="item-tech-news-3"></a>
### [MacBook Pro OLED PWM flicker sparks sensitivity and frequency debate](https://macanorak.com/the-macbook-pros-oled-pwm-problem-when-a-better-display-becomes-worse-to-use/) ⭐️ 7.0/10

An article examines pulse-width-modulation flicker on the MacBook Pro&\#x27;s OLED display and argues that a technically better screen can be worse to use for flicker-sensitive people. In the Hacker News thread, one commenter challenges the cited 240 Hz figure, arguing that the worst case is 480 Hz and that the tandem OLED&\#x27;s two out-of-phase layers can yield an effective 960 Hz across most usable brightness. Other commenters describe broader display sensitivity and call for more research into how many people experience PWM-related problems.

hackernews · MacAnorak · Nov 15, 13:15 · [Discussion](https://news.ycombinator.com/item?id=50506719)

**「Background」** Apple has brought tandem OLED to the MacBook Pro alongside the mini-LED display it has sold since 2021, marketing the new panel as a “PROLED XDR Display.” PWM dimming controls brightness by rapidly switching the panel, and Notebookcheck measured roughly 240 Hz PWM on the OLED model versus about 14,880 Hz on the mini-LED version, so the panel change also changes the flicker characteristics that sensitive users may encounter.

**「What this means for PWM-sensitive buyers」** For PWM-sensitive users, the concrete risk is eye strain or headaches at brightness levels where the panel dims by flickering, even if the OLED screen wins on contrast and color; OLED displays commonly use PWM in the 60–480 Hz range. Because the measured frequency is contested—one commenter argues the tandem OLED runs two 480 Hz layers out of phase for an effective 960 Hz rather than 240 Hz—buyers should test the machine at their normal brightness and confirm the return window instead of relying on a single figure.

**「Community discussion」** Commenters dispute the frequency math: one contends the 240 Hz figure does not account for the tandem OLED&\#x27;s out-of-phase layers and their combined effect, while another finds a low PWM rate surprising for Apple and cites research that flicker can be perceived above twice the display rate. Others widen the discussion to CRI, motion blur, and post-concussion sensitivity, and ask for prevalence data on PWM sensitivity.

<details><summary>References</summary>
<ul>
<li><a href="https://macanorak.com/the-macbook-pros-oled-pwm-problem-when-a-better-display-becomes-worse-to-use/">The MacBook Pro ’s OLED PWM Problem: When a ‘Better’ Display...</a></li>
<li><a href="https://www.notebookcheck.net/Amazing-OLED-panel-Apple-MacBook-Pro-14-PROLED-XDR-Review.1438048.0.html">Amazing OLED panel - Apple MacBook Pro ... - Notebookcheck Review</a></li>
<li><a href="https://www.youtube.com/watch?v=sGgowKoztzk">Is the PROLED ( OLED ) MacBook Pro a Disaster? Flicker ... - YouTube</a></li>
<li><a href="https://trysundown.com/blog/pulse-width-modulation-monitor">PWM Monitor Flicker : Why Your Screen Hurts, and Fixes</a></li>

</ul>
</details>

**Tags**: `#OLED PWM`, `#display flicker`, `#MacBook Pro`, `#hardware ergonomics`, `#Hacker News discussion`

---

<a id="item-tech-news-4"></a>
### [Protomaps PMTiles: cheap self-hosted map tiles for projects](https://bruceroettgers.eu/blog/protomaps/) ⭐️ 7.0/10

A blog post and Hacker News discussion examine how Protomaps, using its PMTiles format, makes self-hosted map tiles affordable and accessible for software projects seeking an alternative to commercial map services. The supplied material does not include the post itself, so specific costs, setup steps, and limitations remain unverified.

hackernews · bcye · Nov 15, 19:26 · [Discussion](https://news.ycombinator.com/item?id=50509837)

**「Background」** Interactive maps are assembled from tiles — square raster images or vector data chunks — that clients fetch as they pan and zoom, and the two common archive formats today are MBTiles and PMTiles. Protomaps packages a customizable world map as a single static file that can be served from cloud storage, the basis for the &quot;serverless&quot; tile-provider setups discussed here.

**「Impact」** For small projects, the practical consequence is cost predictability: one commenter reports that Protomaps made a live-rendered Wikipedia walking game affordable enough to attempt, whereas Mapbox or Google Maps would have ruled it out.

**「Community discussion」** Commenters compare Protomaps with OpenFreeMap, a similar project offering a free public map instance, and describe serving PMTiles from Cloudflare R2 to retain control over privacy and access. They also caution that basemaps are cheap to store, but high-resolution satellite mosaics can reach hundreds of terabytes and become expensive at high zoom levels.

<details><summary>References</summary>
<ul>
<li><a href="https://protomaps.com/">Protomaps - The open source map in a file</a></li>
<li><a href="https://chrisamico.com/blog/2024-02-13/self-hosted-maps/">How to make self - hosted maps that work everywhere and cost next...</a></li>
<li><a href="https://github.com/Rezivure/Grid-Protomaps">Rezivure/Grid- Protomaps : The Protomaps &quot;serverless&quot; map tile ...</a></li>

</ul>
</details>

**Tags**: `#Protomaps`, `#PMTiles`, `#self-hosting`, `#maps`, `#open source`

---

<a id="item-tech-news-5"></a>
### [Sebastian Raschka Explains Positional Embeddings in Modern LLMs](https://magazine.sebastianraschka.com/p/understanding-positional-embeddings) ⭐️ 7.0/10

Sebastian Raschka published a technical explainer on positional embeddings in modern large language models, focused on how these schemes are implemented in transformer architectures. The article was discussed on Hacker News, where the debate centered on its scope rather than on any new result. It is an educational overview: no new method, benchmark, model release, or version change is described.

hackernews · vismit2000 · Nov 15, 12:14 · [Discussion](https://news.ycombinator.com/item?id=50506376)

**「Why LLMs need position signals」** Transformers process tokens in parallel, so order has to be injected explicitly rather than inferred from sequence, typically either added to token embeddings or built into the attention mechanism. GPT-2 used learned absolute position vectors added before the first transformer block, tied to a fixed context of 1,024 positions, while newer architectures have largely moved to rotary position embeddings \(RoPE\). Raschka&\#x27;s walkthrough covers both approaches along with variants such as partial RoPE and NoPE layers, and surveys which scheme individual 2025 and 2026 open-weight models use.

**「Community Discussion」** Commenter programjames argued that the article covers only the implementation of positional embeddings and not the theory, describing positional embeddings as group representations and citing rotary positional embeddings as representations of the translation group, whose abelian structure he says allows them to be derived and parameterized as learnable operations. That is the commenter&\#x27;s view of what deeper understanding requires, not a factual correction to the article&\#x27;s content.

<details><summary>References</summary>
<ul>
<li><a href="https://daily.dev/posts/understanding-positional-embeddings-in-modern-llms-415mglzuo">Understanding Positional Embeddings in Modern LLMs</a></li>
<li><a href="https://sebastianraschka.com/blog/">Blog and Notes - Sebastian Raschka, PhD Positional embeddings in modern LLMs: from GPT-2 to RoPE and ... RoPE vs NoPE: Modern LLM Position Encoding (2026 ... Ahead of AI | Sebastian Raschka, PhD | Substack Sebastian Raschka Explains Positional Embeddings… · AGI Hunt</a></li>

</ul>
</details>

**Tags**: `#positional embeddings`, `#large language models`, `#transformer architecture`, `#deep learning`, `#technical explainer`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Cantor Fitzgerald cut Nvidia stake amid Lutnick ethics scrutiny](https://www.cnbc.com/2026/11/13/howard-lutnick-nvidia-jensen-huang-china-cantor-fitzgerald.html) ⭐️ 8.0/10

CNBC reported that Cantor Fitzgerald, led by Commerce Secretary Howard Lutnick’s sons, reported a 49% decline in its Nvidia share count, to 1.78 million shares at the end of March 2026 from 3.5 million in September 2025, while continuing to arrange financing for Nvidia business partners. The report raises conflict-of-interest questions amid Axios reporting that Lutnick resisted a crackdown on suspected Nvidia chip smuggling to China; CNBC said there is no evidence the holdings change was tied to those warnings.

rss · CNBC Finance · Nov 15, 19:58

**「Background」** Howard Lutnick left Cantor Fitzgerald to become commerce secretary in February 2025, and the firm is now led by his sons, Brandon and Kyle.

**Tags**: `#Nvidia`, `#U.S. export controls`, `#Cantor Fitzgerald`, `#Howard Lutnick`, `#conflict of interest`

---

<a id="item-finance-news-2"></a>
### [U.S. Judge Rejects Dismissal of DRAM Price-Fixing Lawsuit Against Micron, Samsung and SK Hynix](https://www.tomshardware.com/tech-industry/big-tech/judge-denies-motion-to-dismiss-dram-price-fixing-lawsuit-against-micron-samsung-and-sk-hynix-says-chipmakers-acted-like-hawks-flying-in-formation-finds-evidence-of-dram-collusion-plausible-after-500-percent-price-surge) ⭐️ 7.0/10

A U.S. judge denied motions to dismiss a DRAM price-fixing class action against Micron, Samsung and SK Hynix, finding the plaintiffs’ evidence plausible enough for the case to proceed. The plaintiffs allege the three chipmakers made four parallel moves in one year to restrict DRAM supply and that prices rose by as much as 500%; collusion has not been proven.

telegram · zaihuapd · Nov 15, 16:39

**「Background」** The case is a proposed class action by 17 individuals and small businesses alleging that Micron, Samsung and SK Hynix made four parallel moves in a year to restrict DRAM supply and drove prices up by as much as 500%.

<details><summary>References</summary>
<ul>
<li><a href="https://www.techpowerup.com/354863/samsung-sk-hynix-and-micron-fail-to-get-dram-antitrust-suit-dismissed">Samsung , SK hynix , and Micron Fail to Get DRAM Antitrust Suit ...</a></li>

</ul>
</details>

**Tags**: `#DRAM`, `#antitrust`, `#price-fixing`, `#Micron`, `#Samsung`

---

<a id="item-finance-news-3"></a>
### [China, US and Russia to Hold First Trilateral Leaders’ Meeting at Shenzhen APEC](https://apnews.com/article/trump-xi-putin-summit-china-5fe92253ef38100bae913834a9b74d72) ⭐️ 7.0/10

China’s Foreign Ministry announced that the Chinese, US and Russian leaders will meet on Nov. 19 on the sidelines of the APEC summit in Shenzhen. Media reports say it would be their first dedicated trilateral meeting; it is not part of APEC’s official agenda.

telegram · zaihuapd · Nov 16, 01:38

**「Background」** APEC is an Asia-Pacific economic forum, and China&\#x27;s 2026 hosting culminates in the Shenzhen leaders&\#x27; meeting on November 18–19 — the third time China has hosted APEC and the first since 2014.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/APEC_China_2026">APEC China 2026 - Wikipedia</a></li>
<li><a href="https://www.gessymorgan.com/apec-2026-china/">APEC 2026 China: Shenzhen Summit Dates and Agenda</a></li>

</ul>
</details>

**Tags**: `#China-US-Russia relations`, `#APEC summit`, `#geopolitics`, `#diplomatic meeting`

---