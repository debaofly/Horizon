---
layout: default
title: "Horizon Summary: 2026-11-28 (EN)"
date: 2026-11-28
lang: en
---

> From 31 items, 14 important content pieces were selected

---

**Technology News**
1. [OpenSec Discloses Pre-Auth Root Flaw in Linux Kernel NFS Server](#item-tech-news-1) ⭐️ 8.0/10
2. [Google Research&\#x27;s DeepCrossAttention claims up to 3x faster training](#item-tech-news-2) ⭐️ 7.0/10
3. [Essay questions trust in computer-checked proofs over checker soundness bugs](#item-tech-news-3) ⭐️ 7.0/10
4. [States sue SpaceX over Grok&\#x27;s alleged child sexual abuse and revenge-porn images](#item-tech-news-4) ⭐️ 7.0/10
5. [Credit-card skimming scripts using WebRTC reportedly found on shopping sites](#item-tech-news-5) ⭐️ 7.0/10
6. [SemiAnalysis benchmarks AWS Trainium3, claims better perf-per-dollar than GB300](#item-tech-news-6) ⭐️ 7.0/10
7. [Minecraft Bedrock resource-pack flaw affected 26.52–26.63, fixed in 26.65](#item-tech-news-7) ⭐️ 7.0/10
8. [Microsoft plans in-box Windows drivers for printing, audio, and more](#item-tech-news-8) ⭐️ 7.0/10
9. [Convex coding skill accused of undisclosed prompt upload](#item-tech-news-9) ⭐️ 6.0/10
10. [Michael Nielsen&\#x27;s Free Neural Networks Book Taken Down](#item-tech-news-10) ⭐️ 6.0/10
11. [Report: AI Tool Artex Used in Attacks on US Intelligence Agencies](#item-tech-news-11) ⭐️ 6.0/10

**Financial News**
1. [China’s State Council Calls for Stronger State-Backed Market Stabilization Role](#item-finance-news-1) ⭐️ 8.0/10
2. [Mixue to invest RMB 500m in DeepSeek&\#x27;s reported RMB 100bn–105.5bn round](#item-finance-news-2) ⭐️ 7.0/10
3. [China&\#x27;s central bank lowers large-denomination CD minimums](#item-finance-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [OpenSec Discloses Pre-Auth Root Flaw in Linux Kernel NFS Server](https://opensec.in/blog/nfs2root-cve-2026-99362) ⭐️ 8.0/10

OpenSec disclosed CVE-2026-99362, a pre-authentication heap overflow in the Linux kernel&\#x27;s nfsd server rated CVSS 9.8. According to the disclosure, a single connection to tcp/2049 can write out of bounds on the kernel heap and yield a root shell without any login. The flaw is reported to have existed since Linux 3.16 in 2014 and to affect hosts running NFSv4.1 or 4.2, including file servers, NAS devices, and cluster storage nodes. Fixes are listed in kernel releases 6.12.117, 6.18.61, 7.3.2, and 7.4-rc1; administrators must upgrade and reboot, while those unable to do so immediately can restrict tcp/2049 at the firewall. The CVE was published on November 20, 2026.

telegram · zaihuapd · Nov 27, 12:57

**「Background」** nfsd is the Linux kernel&\#x27;s in-kernel NFS server, and hosts serving NFSv4.1 or 4.2—described as the default—listen on TCP port 2049, which is the exposure path for this flaw. OpenSec and Bleeping Computer describe CVE-2026-99362 as a 12-year-old defect, consistent with the source&\#x27;s statement that it has existed since Linux 3.16 in 2014.

**「Patch and reboot, or block tcp/2049」** Any host running nfsd with NFSv4.1 or 4.2 must be upgraded to 6.12.117, 6.18.61, 7.3.2 or 7.4-rc1 and rebooted, since the fix is only active in the running kernel after a restart. Where an immediate kernel upgrade is not possible, administrators must restrict access to tcp/2049 at the firewall, a mitigation that also appears in third-party coverage of the flaw.

<details><summary>References</summary>
<ul>
<li><a href="https://opensec.in/blog/nfs2root-cve-2026-99362">NFS2ROOT ( CVE - 2026 - 99362 ): pre-auth root in Linux nfsd | OpenSec</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/new-nfs2root-linux-flaw-can-let-attackers-gain-root-privileges/">New NFS2ROOT Linux flaw can let attackers gain root privileges</a></li>
<li>Linux users beware — a 12-year-old bug could let hackers gain access ...</li>

</ul>
</details>

**Tags**: `#Linux kernel`, `#NFS`, `#CVE`, `#security vulnerability`, `#pre-auth RCE`

---

<a id="item-tech-news-2"></a>
### [Google Research&\#x27;s DeepCrossAttention claims up to 3x faster training](https://research.google/blog/supercharging-transformer-residual-connections/) ⭐️ 7.0/10

Google Research published a blog post, &quot;Supercharging Transformer Residual Connections,&quot; presenting a method it calls DeepCrossAttention, which modifies Transformer residual connections and attention. The post claims the technique reaches model quality comparable to standard Transformers while running up to 3x faster. The supplied material includes no benchmark numbers, model sizes, baseline details, or code release, and no independent validation of the speedup, so the 3x figure remains a vendor claim rather than a measured result.

hackernews · ComputedCamp995 · Nov 27, 23:06 · [Discussion](https://news.ycombinator.com/item?id=50672565)

**「Background」** Transformer residual connections normally pass each layer’s output forward sequentially, and that structure can dilute information as networks deepen. DeepCrossAttention instead routes information across layers with learnable weights; an arXiv paper describes the architecture as enhancing cross-layer information flow.

**「Implementation Impact」** For teams applying this, DeepCrossAttention is not a drop-in speed switch: it adds three independent GRN instances inside each decoder block, so adoption requires modifying the Transformer block structure. The authors report gains over LAuReL, DenseFormer, and Hyper-Connections on language-modeling benchmarks, but those comparisons come from the paper rather than independent validation.

**「Community Discussion」** Commenters scrutinized the presentation more than the results: one objected that the comparison charts were drawn as line graphs when the methods have no temporal ordering and should be bars, and another asked whether the speedup would compound with existing inference optimizations such as MTP and Dflash derivatives. A further comment likened the approach to DenseNet&\#x27;s dense connectivity, though this is an analogy rather than a confirmed technical correspondence.

<details><summary>References</summary>
<ul>
<li><a href="https://research.google/blog/supercharging-transformer-residual-connections/">Supercharging transformer residual connections</a></li>
<li><a href="https://arxiv.org/html/2502.06785v1">DeepCrossAttention : Supercharging Transformer Residual ...</a></li>
<li><a href="https://arxiv.org/html/2502.06785">DeepCrossAttention : Supercharging Transformer Residual Connections</a></li>
<li><a href="https://www.alphaxiv.org/overview/2502.06785v1">DeepCrossAttention : Supercharging Transformer Residual... | alphaXiv</a></li>

</ul>
</details>

**Tags**: `#transformers`, `#model efficiency`, `#attention mechanisms`, `#Google Research`, `#AI research`

---

<a id="item-tech-news-3"></a>
### [Essay questions trust in computer-checked proofs over checker soundness bugs](https://cr.yp.to/proofs/falseccp.html) ⭐️ 7.0/10

An essay published at cr.yp.to and discussed on Hacker News examines how a proof accepted by a computer proof checker can still be false when the checker itself has a soundness bug. It argues that a single verifier is not sufficient grounds for trust and points to independent verification as a mitigation. The item presents a reliability argument rather than reporting a newly discovered vulnerability, affected version, or newly shipped tool.

hackernews · \_tk\_ · Nov 27, 15:26 · [Discussion](https://news.ycombinator.com/item?id=50667989)

**「Background」** Proof assistants such as Lean and Metamath do not ask readers to trust a long derivation directly; they rely on a small kernel or verifier to check each step against formal rules. A soundness bug in that checker can therefore let an invalid proof be accepted, which is the failure mode Bernstein&\#x27;s essay examines.

**「Impact」** For teams making high-stakes correctness claims with proof assistants, the practical implication is that acceptance by one checker should be treated as conditional on that checker&\#x27;s correctness; where a false claim would be costly, an independently implemented verifier or additional review is warranted.

**「Community discussion」** Commenters agreed that soundness bugs are real but disputed how much they undermine trust: twotwotwo and dwheeler emphasized that independent checkers—including, for Metamath&\#x27;s main databases, five verifiers written in different languages—make a single checker bug insufficient, while gr\_norm called the known bugs rare enough for most software. andai added a separate concern that a proof can be formally valid yet target a mistaken formalization of the requirement.

<details><summary>References</summary>
<ul>
<li><a href="https://cr.yp.to/proofs/falseccp.html">False computer - checked proofs (djb)</a></li>

</ul>
</details>

**Tags**: `#formal-verification`, `#proof-assistants`, `#soundness-bugs`, `#software-correctness`, `#Lean`

---

<a id="item-tech-news-4"></a>
### [States sue SpaceX over Grok&\#x27;s alleged child sexual abuse and revenge-porn images](https://www.oag.state.va.us/media-center/news-releases/jay-jones/3162-attorneys-general-jones-and-rayfield-file-suit-against-spacex-parent-company-of-x-xai-and-grok-over-creation-and-promotion-of-child-exploitation-and-non-consensual-images-on-platform) ⭐️ 7.0/10

Two state attorneys general, identified in the release as Jones and Rayfield, have sued SpaceX, described there as the parent company of X, xAI and Grok, seeking to stop Grok from generating child sexual abuse material and non-consensual intimate images. The complaint also alleges that the platform creates and promotes such content. The release presents the allegations; it reports no court finding and does not specify a hearing date or the scope of the requested injunction.

hackernews · DeepLogin · Nov 27, 19:42 · [Discussion](https://news.ycombinator.com/item?id=50670855)

**「Earlier litigation」** The state action follows a September 2026 lawsuit in which a child sexual abuse survivor alleged that xAI’s Grok used images of her abuse to generate new illegal pornographic images. Unlike that individual claim, the new suit—filed by Oregon and Virginia’s attorneys general—centers on state consumer-protection law and alleges that xAI sidelined consent for growth and engagement.

**「Impact」** The suit creates immediate legal exposure for SpaceX and xAI and, if the requested order is granted, could restrict Grok&\#x27;s image-generation features; the release does not state the injunction&\#x27;s scope or timing.

**「Community Discussion」** Commenters questioned whether Grok was unusually permissive or whether users had to trick it into producing the images, and one asked why the suit targets the platform rather than the people producing them. Another asserted, without citing authority in the thread, that Supreme Court precedent protects AI-generated child sexual abuse material made for personal use while non-consensual images of real people fall outside that protection.

<details><summary>References</summary>
<ul>
<li><a href="https://www.engadget.com/2325111/two-states-sue-spacex-over-sexually-explicit-grok-deepfakes/">Two States Sue SpaceX Over Sexually Explicit Grok Deepfakes</a></li>
<li><a href="https://www.theguardian.com/technology/2026/sep/03/elon-musk-ai-grok-child-porn-lawsuit">Child sexual abuse survivor alleges Elon Musk’s AI... | The Guardian</a></li>

</ul>
</details>

**Tags**: `#AI safety`, `#generative AI`, `#content moderation`, `#AI regulation`, `#xAI/Grok`

---

<a id="item-tech-news-5"></a>
### [Credit-card skimming scripts using WebRTC reportedly found on shopping sites](https://www.infohawk.com/news/2026-11-27-black-friday-webrtc-skimmer) ⭐️ 7.0/10

A report claims that credit-card skimming scripts using WebRTC were found on popular shopping sites, raising third-party script risk for online shoppers and site operators. The supplied account does not name the affected sites, describe the scripts, or quantify user exposure, so the finding should be treated as reported rather than independently confirmed.

hackernews · scanr · Nov 27, 15:40 · [Discussion](https://news.ycombinator.com/item?id=50668145)

**「Background」** WebRTC is a browser API for real-time audio, video, and data connections, and commenters argued that its role in this reported skimming campaign is less about a WebRTC-specific flaw than about monitoring gaps around its traffic. The recurring exposure is third-party JavaScript embedded in checkout pages: if an external script is compromised, it can access payment-form data. The supplied item gives no technical detail on how the reported scripts actually used WebRTC, so that mechanism remains unconfirmed.

**「Third-party checkout script risk」** For online retailers, the reported WebRTC skimming scripts make third-party JavaScript on checkout pages part of the card-data attack surface; operators should inventory and restrict scripts that can read payment forms rather than treat a single browser-API block as sufficient. A separate November 2026 incident showed malicious JavaScript planted in a third-party platform reaching visitors of 178 organizations, illustrating why the embedded dependency itself is the control point.

**「Community discussion」** Commenters argued that ad blocking is a reasonable defense because embedded third-party scripts are the weak point, while one noted that the WebRTC angle reflects less monitoring and harder-to-detect mobile targeting rather than a unique technical capability. Others called for ad code to be sandboxed or for browsers to render ads without executing JavaScript.

<details><summary>References</summary>
<ul>
<li><a href="https://cybersecuritynews.com/optimizely-websites-hijacked/">Hackers Infect 178 Major Websites via Optimizely to Steal Credit ...</a></li>

</ul>
</details>

**Tags**: `#web security`, `#credit card skimming`, `#WebRTC`, `#third-party scripts`, `#e-commerce`

---

<a id="item-tech-news-6"></a>
### [SemiAnalysis benchmarks AWS Trainium3, claims better perf-per-dollar than GB300](https://newsletter.semianalysis.com/p/trainium3-inferencex) ⭐️ 7.0/10

SemiAnalysis published a deep dive on AWS Trainium3&\#x27;s inference performance, reporting that on its InferenceX benchmark the chip, running with PDS and vLLM, achieves better performance per dollar of total cost of ownership than every accelerator tested except Nvidia&\#x27;s Vera Rubin across the TCO-versus-p90-interactivity curve, and trades blows with or even beats Nvidia GB300 on token-generation cost. The analysis credits part of the gap to Trainium&\#x27;s tile-first microarchitecture: UBenchX microbenchmarks found Trainium reaching peak HBM bandwidth utilization at small message sizes through its Descriptor Generation Engines \(DGE\), AWS&\#x27;s counterpart to Nvidia&\#x27;s TMA, which the authors say is not achievable on Nvidia GPUs. The post also covers cycle-level SRAM scratchpad latency and bandwidth \(SBUF to PSUM\), rack-scale bandwidth and latency, and attention exponential behavior across head dimensions, but the supplied excerpt offers few absolute numbers or methodology details. The results are SemiAnalysis&\#x27;s own measurements, produced with help from AWS Annapurna Labs co-founder Nafea Bshara and Trainium chief architect Ron Diamant, so they are best read as vendor-assisted third-party benchmarks rather than independent verification.

rss · Semianalysis · Nov 27, 15:54

**「Background」** Trainium is AWS&\#x27;s in-house AI accelerator line, designed by its Annapurna Labs chip unit, and Trainium3 is the third generation of that family. Earlier generations were widely seen as hardware with potential held back by an immature software stack; the SemiAnalysis piece notes this had been &quot;a humongous challenge&quot; and argues it no longer is. AWS has separately committed to the line at scale: an April 2026 announcement paired up to $25B in additional Anthropic investment with a $100B Trainium/Graviton commitment.

**「What this means for accelerator buyers」** Teams choosing hardware for token generation now have a published, workload-specific cost curve for Trainium3: SemiAnalysis reports its PDS + vLLM stack beats every accelerator except Vera Rubin on performance per TCO across the latency-throughput frontier, measured on GLM-5 and on replayed coding-agent sessions. That makes Trainium3 a credible second source for cost-sensitive inference, but the result is tied to that specific software path — the article concedes Trainium&\#x27;s ML-first design historically made software a major obstacle — and it stops short of Vera Rubin. Buyers should re-measure on their own model shapes, including attention head\_dim, rather than assume the published frontier transfers.

<details><summary>References</summary>
<ul>
<li><a href="https://www.idlen.io/news/amazon-anthropic-25-billion-investment-100-billion-aws-trainium-april-2026/">Amazon Pours Another $25B Into Anthropic — $100B AWS Trainium ...</a></li>
<li><a href="https://au.finance.yahoo.com/news/aws-annapurna-labs-global-ai-100500331.html">AWS Annapurna Labs Global AI, Compute, Data, and Quantum...</a></li>

</ul>
</details>

**Tags**: `#AWS Trainium`, `#AI hardware`, `#inference`, `#microarchitecture`, `#Nvidia`

---

<a id="item-tech-news-7"></a>
### [Minecraft Bedrock resource-pack flaw affected 26.52–26.63, fixed in 26.65](https://www.zaikei.co.jp/article/20261119/878386.html) ⭐️ 7.0/10

A resource-pack vulnerability in Minecraft Bedrock let packages containing a content.zipe file alter files in the Ore UI interface framework and run hidden scripts. Developer 8Crafter disclosed it on November 15 and confirmed it affected versions 26.52 through 26.63, with earlier versions possibly also affected, on PC, mobile, and consoles; Java Edition was not affected. When resource-pack auto-download was enabled on servers or Realms, players could receive a malicious pack without manually installing it; reported exploits included deleting all saves, obtaining a player&\#x27;s IP address, and, under certain Windows conditions, silently opening arbitrary URIs and launching batch files in the pack to download malware. Mojang fixed the issue in version 26.65, and AxmBro released a read-only Windows detection tool that finds content.zipe files but cannot determine whether a pack is malicious.

telegram · zaihuapd · Nov 27, 18:04

**「Background」** Bedrock Edition resource packs are client-side packages that can replace textures, models, and interface files, and the Ore UI framework renders the game&\#x27;s menus and on-screen interface. Servers and Realms can offer resource packs for automatic download, so a crafted pack can reach players without a separate manual install step. The reported flaw involved a content.zipe file inside such a pack that could modify Ore UI files and run hidden scripts.

**「Update and turn off auto-download」** Players joining servers or Realms with resource-pack auto-download enabled can receive a crafted pack without installing anything, and 8Crafter&\#x27;s listed outcomes include deleted saves, exposed IP addresses, and — on Windows under specific conditions — silent opening of arbitrary URIs and launching batch files that download malware. Updating to 26.65 is the direct fix, but because auto-download is the delivery path, disabling it on untrusted servers adds protection until clients are patched. AxmBro&\#x27;s Windows scanner only flags the presence of a content.zipe file and cannot judge whether a pack is malicious, so it should not be treated as a clean bill of health.

**Tags**: `#Minecraft Bedrock`, `#resource pack vulnerability`, `#security`, `#Ore UI`, `#malware`

---

<a id="item-tech-news-8"></a>
### [Microsoft plans in-box Windows drivers for printing, audio, and more](https://www.techspot.com/news/114721-microsoft-wants-replace-most-third-party-device-drivers.html) ⭐️ 7.0/10

At Ignite 2026, Microsoft confirmed it is developing new Windows in-box drivers for entire hardware classes, aiming to keep more third-party code out of the kernel. Printing is the first focus: the recently introduced Windows Ready Print mode is intended to replace legacy third-party print drivers. Microsoft product manager Mehmet Kucukgoz said SoundWire and SDCA audio drivers will soon become Windows components, while I3C bus, USB Ethernet, and MIPI camera drivers are in development. Microsoft also launched a Driver Quality Initiative \(DQI\) to raise reliability, quality, and security standards and is encouraging third-party developers and OEMs to rely on in-box drivers where possible.

telegram · zaihuapd · Nov 28, 02:09

**「Background」** Windows has traditionally relied on third-party kernel-mode drivers for device classes such as printing and audio, so moving those classes in-box reduces the amount of third-party code running in the kernel. The printing portion follows Microsoft’s Windows Ready Print effort: Windows Forum reported that, starting in July 2026, supported new printer installations will prefer IPP-based printing using the built-in Windows IPP printer driver.

**「Impact」** Printer and audio vendors and OEMs face the most immediate work: they should validate existing hardware against the in-box driver paths, since Ready Print already targets legacy printing and SoundWire/SDCA support is slated to move into Windows. Microsoft has not announced a timeline for replacing drivers in the other classes, so custom-driver work for those areas cannot yet be treated as obsolete.

<details><summary>References</summary>
<ul>
<li><a href="https://windowsforum.com/threads/windows-ready-print-in-july-2026-ipp-inbox-printing-policy-controls-protected-mode.425059/">Windows Ready Print in July 2026 : IPP Inbox ... | Windows Forum</a></li>

</ul>
</details>

**Tags**: `#Windows`, `#device drivers`, `#Microsoft`, `#kernel security`, `#hardware support`

---

<a id="item-tech-news-9"></a>
### [Convex coding skill accused of undisclosed prompt upload](https://github.com/convex/convex-backend-skill/issues/64) ⭐️ 6.0/10

A GitHub issue \(\#64\) against convex/convex-backend-skill alleges that the Convex coding skill sends users&\#x27; app ideas to a remote server without disclosing the upload. Convex CEO Jamie responded in the thread that the plugin&\#x27;s prompt upload powers Convex&\#x27;s “quickstart” feature, which he described as the spiritual successor to the recently shut-down Convex Chef, and that Convex operates a full platform storing customer data and code plus an AI gateway. The exchange centers on whether that upload is adequately disclosed; the supplied material does not include the plugin&\#x27;s disclosure text or an independent technical audit.

hackernews · MickyTheMouse · Nov 27, 18:02 · [Discussion](https://news.ycombinator.com/item?id=50669765)

**「Background」** Convex Chef was an earlier Convex project that generated full-stack apps from AI prompts, built on the company&\#x27;s reactive database and APIs. In the issue thread, Convex CEO Jamie said Chef was shut down recently and that the prompt upload in question now powers the newer &quot;quickstart&quot; feature, which he described as Chef&\#x27;s spiritual successor.

**「Data-flow risk for Convex skill users」** Developers using the Convex coding skill should treat app ideas and prompts as data that may leave their machine: Convex&\#x27;s CEO says the plugin&\#x27;s prompt upload powers the quickstart feature, so teams should check the skill&\#x27;s disclosure and avoid entering proprietary concepts or secrets until the remote data flow is clearly documented.

**「Community discussion」** Commenters treated the report as a trust and transparency test for AI developer tooling. One said self-hosted open-weight models are the long-term path, and another argued prompt injection is far more common than models making malicious tool calls on their own, without concluding this case was malicious.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/convex/chef">GitHub - convex / chef : The only AI app builder that knows backend</a></li>

</ul>
</details>

**Tags**: `#privacy`, `#AI developer tooling`, `#prompt upload`, `#vendor transparency`, `#security`

---

<a id="item-tech-news-10"></a>
### [Michael Nielsen&\#x27;s Free Neural Networks Book Taken Down](https://neuralnetworksanddeeplearning.com/) ⭐️ 6.0/10

Michael Nielsen&\#x27;s free online book Neural Networks and Deep Learning has been taken down from neuralnetworksanddeeplearning.com, according to a Hacker News post dated Nov. 27, 2026. The supplied material does not include Nielsen&\#x27;s stated reason for the removal, and no author-hosted replacement is noted. The removal directly affects learners who used the site as a widely used free introduction to neural networks; a commenter linked a web-archive copy of the book.

hackernews · brandonb · Nov 27, 19:31 · [Discussion](https://news.ycombinator.com/item?id=50670757)

**「What the book was」** Neural Networks and Deep Learning is Michael Nielsen&\#x27;s free online book, hosted at neuralnetworksanddeeplearning.com, which teaches the core concepts behind neural networks and deep learning from an introductory level. Because it was freely readable on the open web, PDF copies and mirrors of the text circulated independently of the author&\#x27;s own site, so the material was never confined to a single URL.

**「Effect on learners」** Readers who relied on the free online edition as a primary learning reference lose the canonical site for it, and instructors who link to or assign the book will need to point students elsewhere. A commenter posted an Internet Archive snapshot, so the text remains reachable through mirrors, but discoverability and any stable citation to the original URL are disrupted.

**「Community Discussion」** Commenters disagreed over the removal&\#x27;s purpose and effect: one argued that teaching people how neural networks work helps them understand what large companies are doing, while another characterized the takedown as more symbolic protest than practical restriction and predicted it would push more people to find the book elsewhere. A separate thread debated AI risk and whether current systems already amount to ASI.

<details><summary>References</summary>
<ul>
<li><a href="http://neuralnetworksanddeeplearning.com/">Neural networks and deep learning</a></li>
<li><a href="https://jingyuexing.github.io/Ebook/Machine_Learning/Neural+Networks+and+Deep+Learning-eng.pdf">1 Neural networks and deep learning .pdf</a></li>
<li><a href="http://neuralnetworksanddeeplearning.com/">Neural networks and deep learning</a></li>

</ul>
</details>

**Tags**: `#AI safety`, `#neural networks`, `#open educational resources`, `#tech community`, `#AI industry`

---

<a id="item-tech-news-11"></a>
### [Report: AI Tool Artex Used in Attacks on US Intelligence Agencies](https://www.forbes.com/sites/the-wiretap/2026/11/25/us-government-under-ai-cyberattack) ⭐️ 6.0/10

Reports relayed in a Telegram post say hackers used an AI tool called Artex in attacks on the CIA, the National Geospatial-Intelligence Agency and the Office of the Director of National Intelligence; the reported impact was limited to non-classified reconnaissance data and the intrusion appeared not to be severe. According to the post, which cites The New York Times and Forbes, Artex can combine multiple open-source AI models to test network and computer defenses. A Chinese developer released the tool earlier this year and later deleted it from GitHub after it was used in several attacks, including one against the EU, the post says; it also says the FBI warned earlier this year that criminals and spies were widely using Artex. The supplied item provides limited technical detail and no independent verification of the claims.

telegram · zaihuapd · Nov 27, 10:42

**「Background」** Artex is an AI-powered penetration-testing framework that can integrate multiple AI models, including frontier and open-source or Chinese-origin models, to automate network attacks. The FBI had already warned that it was being used in attacks, including a ConnectWise supply-chain breach that compromised Microsoft 365 customer environments; after those attacks, its developer made the tool closed-source, but the FBI said the earlier open-source version remained widely accessible.

**「Contained exposure, persistent tooling」** The reported breach exposed non-classified reconnaissance data at the CIA, National Geospatial-Intelligence Agency and Office of the Director of National Intelligence, so the immediate damage appears limited to unclassified material rather than classified sources or methods. The developer&\#x27;s deletion of Artex from GitHub came only after the tool had been used in multiple attacks, including one linked to the theft of 8.2 million records, so removing the repository does not by itself take the capability out of circulation.

<details><summary>References</summary>
<ul>
<li><a href="https://techcrunch.com/2026/11/16/fbi-says-artex-ai-open-source-hacking-tool-used-to-breach-networks-in-under-three-hours/">FBI says Artex AI open source hacking tool used to... | TechCrunch</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/fbi-warns-artex-ai-hacking-tool-is-powering-global-cyberattacks/">FBI warns ARTEX AI hacking tool is powering global cyberattacks</a></li>
<li><a href="https://therecord.media/artex-ai-tool-fbi-flash-alert">FBI flash alert says Artex tool automating cyberattacks at ‘machine...</a></li>
<li><a href="https://rurtnews.com/news/649360-nyt-cia-artex-hack/">CIA , other US spy agencies hit by new hack – NYT — RT World News</a></li>
<li><a href="https://www.forbes.com/sites/the-wiretap/2026/11/25/us-government-under-ai-cyberattack/">The US Government Is Under AI Cyberattack</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/former-pentester-used-artex-ai-to-steal-82-million-data-records/">Former pentester used ARTEX AI to steal 8.2 million data records</a></li>

</ul>
</details>

**Tags**: `#AI cybersecurity`, `#cyberattacks`, `#open-source AI`, `#threat intelligence`, `#US government`

---

## Financial News

<a id="item-finance-news-1"></a>
### [China’s State Council Calls for Stronger State-Backed Market Stabilization Role](https://www.tmtpost.com/nictation/8220182.html) ⭐️ 8.0/10

A State Council executive meeting chaired by Premier Li Qiang on Nov. 27 called for a stronger role for the state-backed “national team” in stabilizing China’s stock market and for optimizing Central Huijin’s quasi-“stabilization fund” function, alongside support policies to guide insurance, corporate annuity and social security funds into the market. The readout gave no fund size, tool details or implementation timetable, so these remain policy directions rather than announced market operations.

telegram · zaihuapd · Nov 27, 05:35

**「背景」** “国家队”通常指中央汇金公司等有国家背景的入市资金；所谓“平准基金”，是政府背景资金通过买卖股票来平抑市场大幅波动的工具，中央汇金目前承担的是“类”平准基金职能，而非名义上的平准基金。

**Tags**: `#中国资本市场`, `#国务院常务会议`, `#中央汇金`, `#平准基金`, `#中长期资金`

---

<a id="item-finance-news-2"></a>
### [Mixue to invest RMB 500m in DeepSeek&\#x27;s reported RMB 100bn–105.5bn round](https://m.sohu.com/a/1107027659_115479) ⭐️ 7.0/10

Mixue Ice City has reportedly agreed to invest RMB 500 million in DeepSeek as part of a second financing round of roughly RMB 100 billion to RMB 105.5 billion, at a post-money valuation of about RMB 615.5 billion, according to a Sohu report.

telegram · zaihuapd · Nov 27, 06:33

**「Background」** The Information reported that DeepSeek raised about RMB 51bn in a first funding round in June, so this second round of roughly RMB 105.5bn is about twice that size \(tool-1-1\). The ~RMB 615.5bn figure is a post-money valuation, meaning the company&\#x27;s assessed worth after the new money is counted.

**「What it means」** The reported RMB500m fund commitment would give Mixue indirect exposure to DeepSeek, tying part of the beverage chain’s capital to the AI startup’s valuation.

<details><summary>References</summary>
<ul>
<li><a href="https://www.ithome.com/1/020/121.htm">曝 DeepSeek 第 二 轮 融 资 1055 亿 元 ： 估 值 6155 ...</a></li>

</ul>
</details>

**Tags**: `#DeepSeek`, `#Mixue`, `#venture financing`, `#AI`, `#valuation`

---

<a id="item-finance-news-3"></a>
### [China&\#x27;s central bank lowers large-denomination CD minimums](https://www.news.cn/fortune/20261127/70789d77822242cc82216f51a416f872/c.html) ⭐️ 7.0/10

The People&\#x27;s Bank of China published new large-denomination certificate of deposit rules on Nov. 27, lowering the individual minimum purchase to 100,000 yuan from 200,000 yuan and the institutional minimum to 5 million yuan from 10 million yuan, effective March 21, 2027.

telegram · zaihuapd · Nov 27, 11:36

**「Background」** The new measures replace 2015 interim rules, and they take effect alongside separate PBOC rules requiring financial institutions to set RMB deposit and lending rates independently and barring improper high-interest deposit-taking.

**「Impact」** The lower individual floor brings savers with 100,000 to 200,000 yuan into eligibility for large-denomination CDs, while the pricing rules bar banks from using improper high-interest offers to attract deposits.

**Tags**: `#大额存单`, `#中国人民银行`, `#存款利率`, `#银行监管`, `#个人储蓄`

---