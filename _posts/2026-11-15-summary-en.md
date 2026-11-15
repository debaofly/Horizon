---
layout: default
title: "Horizon Summary: 2026-11-15 (EN)"
date: 2026-11-15
lang: en
---

> From 39 items, 7 important content pieces were selected

---

**Technology News**
1. [Lovable-built apps exposed passports and 200K+ private messages](#item-tech-news-1) ⭐️ 8.0/10
2. [EFF: Tech companies are trying to shift the concept of privacy again](#item-tech-news-2) ⭐️ 7.0/10
3. [Project Zero sets 90-day disclosure, shrinking to 30 by 2028](#item-tech-news-3) ⭐️ 7.0/10
4. [Show HN: DeepSeek V3 in About 200 Lines of Pure JAX](#item-tech-news-4) ⭐️ 7.0/10
5. [Starship Flight 15 returns ship to tower, booster lost](#item-tech-news-5) ⭐️ 7.0/10
6. [Cloudflare open-sources Kitesurf, a stateless browser for AI agents](#item-tech-news-6) ⭐️ 7.0/10
7. [Italy fines Meta €805M over Facebook Android photo access](#item-tech-news-7) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Lovable-built apps exposed passports and 200K+ private messages](https://www.crissyfield.de/research/lovable-en/) ⭐️ 8.0/10

Security research published by Crissy Field reports that apps built with Lovable exposed passport details and more than 200,000 private messages because of insufficient Row-Level Security. In the Hacker News thread, Lovable&\#x27;s head of security said the root cause was insufficient RLS and that the company scans every app before publish, offers a free deeper SAST scan, and lets users fix findings, enable auto-fix, or block publishing. The report&\#x27;s author said the post had been submitted earlier but gained little traction; the supplied material does not include the full write-up or independent confirmation of the exposure count.

hackernews · armcat · Nov 14, 17:43 · [Discussion](https://news.ycombinator.com/item?id=50499017)

**「Background」** Row-Level Security is Postgres&\#x27;s mechanism for restricting which rows a client can read or write, and Supabase&\#x27;s Data API can reach public-schema tables through client-side keys. Supabase has faced long-running complaints that anon-key database access is hard to revoke, and it changed its defaults on 30 October 2026 so new public tables are no longer automatically granted to the anon, authenticated and service\_role roles. Apps without correctly configured RLS policies can therefore leave rows exposed through the Data API.

**「Impact」** Developers publishing Lovable apps with a Supabase backend should verify Row-Level Security policies and use the available pre-publish and SAST scans, because insufficient RLS can leave private records exposed through the app&\#x27;s database API.

**「Community discussion」** Commenters focused on Supabase&\#x27;s role, arguing that permissive defaults traded easier onboarding for weaker security; one said the issue was supposedly fixed on October 30 but that reports suggest existing projects may still use the old defaults. Others described these AI-generated apps as easy and numerous targets and called for deny-by-default databases, least-privilege APIs, and automated authentication tests.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/orgs/supabase/discussions/4547">Option to disable anon key access to database · supabase ...</a></li>
<li><a href="https://www.putthrough.com/blog/supabase-permission-denied-for-table">Supabase “permission denied for table” (42501): the safe fix</a></li>

</ul>
</details>

**Tags**: `#security research`, `#row-level security`, `#Supabase`, `#AI app builders`, `#data exposure`

---

<a id="item-tech-news-2"></a>
### [EFF: Tech companies are trying to shift the concept of privacy again](https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again) ⭐️ 7.0/10

The Electronic Frontier Foundation published a Nov. 14, 2026 analysis arguing that technology companies are making another attempt to redefine what privacy means, treating the reframing itself as the policy fight rather than any single product. The available excerpt does not name the specific companies, products, or proposals EFF examines, so the concrete scope of the claimed redefinition is not established here. The Hacker News thread that formed around the piece focused less on the article&\#x27;s argument than on AI meeting notetakers and whether workers can refuse to be recorded.

hackernews · gslin · Nov 14, 12:45 · [Discussion](https://news.ycombinator.com/item?id=50496602)

**「Background」** The Electronic Frontier Foundation, which published this piece on its deeplinks blog, is a nonprofit digital rights organization that describes its work as defending privacy and free expression on the argument that technology should serve all people, not just the powerful. That advocacy role frames the item: it is an argument about how technology companies define and redefine privacy, rather than the announcement of a specific product or regulatory change.

**「Workplace exposure」** The people most immediately affected are employees whose meetings are joined by AI notetakers: as commenters describe it, declining is not a default, so the practical burden falls on individuals to ask that recording stop and on employers to set an explicit policy on when notetakers may join and how long transcripts are kept. Without such a default, each worker has to negotiate exposure case by case, including in one-on-one meetings with managers.

**「Community discussion」** Commenter toddmorey described every professional meeting, including 1:1s with direct managers, being recorded and uploaded by seen and unseen AI guests, and asked whether anyone has normalized saying &quot;transcription isn&\#x27;t needed for this meeting&quot; before proceeding, since opting out feels impossible while staying employed. abecedarius argued that well-implemented live transcription could be transformative for deaf and hard-of-hearing users and noted a local model need not save or export anything, while Papazsazsa proposed compartmentalized identities, air gaps, and EFF membership as partial practical mitigations.

<details><summary>References</summary>
<ul>
<li><a href="https://www.eff.org/">Electronic Frontier Foundation | Defending your rights in the ...</a></li>

</ul>
</details>

**Tags**: `#privacy`, `#AI surveillance`, `#tech policy`, `#data protection`, `#workplace AI`

---

<a id="item-tech-news-3"></a>
### [Project Zero sets 90-day disclosure, shrinking to 30 by 2028](https://projectzero.google/2026/11/disclosure-policy.html) ⭐️ 7.0/10

Google Project Zero is moving to a staged vulnerability-disclosure policy: 90 days after reporting a flaw, then 60 days on Feb. 2, 2027, and 30 days on Jan. 3, 2028. A comment that quotes the announcement gives those dates and labels the phases “Full 90,” “Full 60,” and “Full 30.” The policy governs when Project Zero publishes vulnerability details after notifying vendors, giving software maintainers progressively less time to patch before disclosure. The evidence available is the announcement and comment excerpts, not an independent measure of vendor patch times.

hackernews · hacb · Nov 14, 11:13 · [Discussion](https://news.ycombinator.com/item?id=50496051)

**「Background」** Project Zero previously used a “90+30” disclosure model, a policy that was already being debated in 2021. The new schedule replaces that framework, starting with an immediate “Full 90” window and later shortening the deadline to 60 days in February 2027 and 30 days in January 2028.

**「Impact」** Vendors and open-source maintainers will have to complete fixes and coordinated releases within 60 days after February 2027 and 30 days after January 2028; a commenter singled out Ubuntu as needing “a LOT more time.”

**「Community Discussion」** Commenters disagreed about whether the shorter windows are workable: one said Ubuntu will need much more time, while another argued for immediate disclosure because only public pressure compels vendors to fix flaws.

<details><summary>References</summary>
<ul>
<li><a href="https://cje.io/2021/05/08/on-project-zeros-90-30-vulnerability-disclosure-policy-changes/">On Project Zero &#x27;s 90 + 30 vulnerability disclosure policy changes</a></li>

</ul>
</details>

**Tags**: `#vulnerability disclosure`, `#cybersecurity`, `#Project Zero`, `#Google`, `#software security`

---

<a id="item-tech-news-4"></a>
### [Show HN: DeepSeek V3 in About 200 Lines of Pure JAX](https://github.com/Vaibhaav-Tiwari/deepseek-v3-jax) ⭐️ 7.0/10

A Show HN project by VaibhaavTiwari reimplements DeepSeek V3 in roughly 200 lines of pure JAX, offering a small codebase for studying LLM inference and experimenting locally. The scope points to a focused or simplified implementation rather than a production-grade release. A commenter reported running it end-to-end on an AMD RX 7600 XT 16GB under Fedora with ROCm, which required setting HSA\_OVERRIDE\_GFX\_VERSION=11.0.0 because JAX&\#x27;s plugin rejects gfx1102.

hackernews · VaibhaavTiwari · Nov 14, 15:04 · [Discussion](https://news.ycombinator.com/item?id=50497589)

**「Background: JAX, ROCm and from-scratch model code」** DeepSeek V3 is a large language model from DeepSeek, and rewriting such a model&\#x27;s forward pass from scratch in a compact script is a common way for engineers to study inference internals rather than call a packaged library. JAX is Google&\#x27;s NumPy-style array and automatic-differentiation library, which compiles code through XLA and can target GPUs via backends other than CUDA, including AMD&\#x27;s ROCm stack. That portability is what the project&\#x27;s commenters tested: one reported running the code end-to-end on an RX 7600 XT 16GB using ROCm, noting it needed the HSA\_OVERRIDE\_GFX\_VERSION environment variable because JAX&\#x27;s plugin did not recognize the card&\#x27;s gfx1102 target.

**「Impact」** For developers on AMD GPUs, the report gives a concrete compatibility path: JAX rejected the RX 7600 XT&\#x27;s gfx1102 target until HSA\_OVERRIDE\_GFX\_VERSION=11.0.0 was set, so similar setups may need the same override. The evidence is a single user&\#x27;s Fedora and ROCm configuration, not a tested support matrix.

**「Community discussion」** Commenters welcomed the project as a first-principles way to learn how inference works. One reader comfortable with Java and Python asked for a roadmap to build that intuition, and another said they would recreate it for study.

**Tags**: `#DeepSeek V3`, `#JAX`, `#LLM inference`, `#ROCm`, `#open-source code`

---

<a id="item-tech-news-5"></a>
### [Starship Flight 15 returns ship to tower, booster lost](https://www.spacex.com/launches/starship-flight-15) ⭐️ 7.0/10

SpaceX launched Starship Flight 15 from Texas on November 13 and announced that the orbital-class ship returned after about 22.5 hours and 14 orbits, then was caught by the launch tower&\#x27;s arms for the first time. The flight deployed all 26 Starlink V3 satellites, three of which carried cameras to inspect the heat shield. The Super Heavy booster aborted its return to the tower, made a controlled splashdown in the Gulf of Mexico and exploded; SpaceX did not disclose the cause, so the planned dual tower catch was not achieved.

telegram · zaihuapd · Nov 14, 03:03

**「Background」** Flight 15 was the 15th Starship test and used Super Heavy booster 22 and ship 42, both V3 vehicles, launching from Starbase on Nov. 13. SpaceX’s recovery plan relies on the launch tower’s mechanical arms catching a returning vehicle at a designated catch point rather than landing it on legs or at sea. Before the flight, CNN reported that the V3 Super Heavy had experienced stubborn engine issues that occasionally caused some of its 33 engines to flame out prematurely.

**「Impact」** The ship catch demonstrates the recovery step needed to reuse an orbital-class Starship, but the booster loss leaves SpaceX without simultaneous recovery of both stages, the condition its dual-catch plan was meant to prove.

<details><summary>References</summary>
<ul>
<li><a href="https://www.youtube.com/watch?v=qESAelVjYsE">Texas Coast: Giant Rocket Booster Blows Up in... - YouTube</a></li>
<li><a href="https://www.cnn.com/2026/11/13/science/live-news/spacex-starship-flight-15-ship-catch">Live updates: SpaceX Starship nails historic ship catch in... | CNN</a></li>

</ul>
</details>

**Tags**: `#SpaceX`, `#Starship`, `#spaceflight`, `#reusable rockets`, `#Starlink`

---

<a id="item-tech-news-6"></a>
### [Cloudflare open-sources Kitesurf, a stateless browser for AI agents](https://www.phoronix.com/news/Cloudflare-Kitesurf-Open-Source) ⭐️ 7.0/10

Cloudflare has open-sourced Kitesurf under the Apache 2.0 license, describing it as a stateless browser for AI agents. Built on Cloudflare Workers, it parses HTML, handles CSS, and executes JavaScript without a browser container. Cloudflare says it uses less CPU and memory than Chromium and can scale across its global Workers network, but the source provides no benchmarks or independent validation. The code is available on GitHub.

telegram · zaihuapd · Nov 14, 09:33

**「Background」** AI agents that browse the web commonly need to fetch a page, apply CSS, and execute JavaScript; conventional headless-browser setups do this by running a full engine such as Chromium inside a container. Kitesurf&\#x27;s premise is to provide that page-processing path as a stateless service on Cloudflare Workers, avoiding a persistent browser container.

**「Impact」** Teams running agent-driven page automation can avoid provisioning Chromium containers, since Kitesurf runs as a stateless Workers-based engine that Cloudflare says uses less CPU and memory and scales on its global network. Because it handles HTML, CSS, and JavaScript itself rather than being a full browser, teams should validate that their target pages render correctly under Kitesurf before replacing an existing headless-Chromium pipeline.

**Tags**: `#Cloudflare`, `#AI agents`, `#browser`, `#open source`, `#Cloudflare Workers`

---

<a id="item-tech-news-7"></a>
### [Italy fines Meta €805M over Facebook Android photo access](https://www.garanteprivacy.it/home/docweb/-/docweb-display/docweb/10321080) ⭐️ 7.0/10

Italy’s Garante Privacy fined Meta €805 million, saying the Facebook Android app accessed the photos, videos and metadata of about 20 million Italian users without specific consent. The regulator ordered Meta to change the album-recommendation feature—launched in 2023, on by default and presented with a generic permission prompt—within 60 days so that it is off by default and obtains separate consent; otherwise, it must not be enabled for users without valid authorization.

telegram · zaihuapd · Nov 14, 14:37

**「Background」** The case concerns an album-recommendation feature that Meta added to the Facebook Android app in 2023; it shipped enabled by default and presented users with only a generic permission prompt rather than a specific request to access their photos, videos and metadata. Italy&\#x27;s Garante per la protezione dei dati personali is the national authority that enforces data-protection rules against services used in the country, which is why the order and the 60-day deadline for changing the default setting and consent flow fall to it.

**「Impact」** Meta must redesign the feature’s Android consent flow for Italian users within 60 days: album recommendations cannot be enabled without a separate, valid opt-in.

**Tags**: `#Meta`, `#隐私监管`, `#数据保护`, `#Android`, `#合规`

---