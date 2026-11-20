---
layout: default
title: "Horizon Summary: 2026-11-20 (EN)"
date: 2026-11-20
lang: en
---

> From 34 items, 11 important content pieces were selected

---

**Technology News**
1. [PostgreSQL 19 ships with WAIT FOR LSN for standby reads](#item-tech-news-1) ⭐️ 9.0/10
2. [Anthropic’s Nasdaq debut](#item-tech-news-2) ⭐️ 8.0/10
3. [PHP mixed-case HTTPS/FTPS schemes silently disabled TLS](#item-tech-news-3) ⭐️ 8.0/10
4. [Anthropic claims Claude helped solve two black-hole physics problems](#item-tech-news-4) ⭐️ 7.0/10
5. [European Commission Deploys Matrix to 40,000+ Staff, Element Says](#item-tech-news-5) ⭐️ 7.0/10
6. [OpenJDK &\#x27;java4shell&\#x27; PR debate centers on Oracle takeover and AI discovery](#item-tech-news-6) ⭐️ 7.0/10
7. [UK government admits secret encryption order to Apple](#item-tech-news-7) ⭐️ 7.0/10
8. [PHP plans CRITICAL security release for supported versions](#item-tech-news-8) ⭐️ 7.0/10
9. [OpenAI says models aided Jalapeño, AMD GPU design; AMD PPA up to 14%](#item-tech-news-9) ⭐️ 7.0/10
10. [Gemini can now operate Macs for US subscribers, with background runs and pause controls](#item-tech-news-10) ⭐️ 7.0/10

**Financial News**
1. [Asian stocks fall as doubts about AI spending grow after Anthropic IPO](#item-finance-news-1) ⭐️ 8.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [PostgreSQL 19 ships with WAIT FOR LSN for standby reads](https://simonwillison.net/2026/Nov/19/postgresql-19/) ⭐️ 9.0/10

PostgreSQL 19 has been released, about two months later than its usual September cadence; Simon Willison attributes the delay mainly to issues the team handled during the ongoing wave of AI-reported vulnerabilities. The release adds WAIT FOR LSN, which lets a session on a standby wait until the standby has replayed the write-ahead log through a specified log sequence number before running a query, providing read-your-writes consistency for reads sent to replicas. An application can capture pg\_current\_wal\_insert\_lsn\(\) after a write on the primary, store that value, and then run WAIT FOR LSN &\#x27;0/0306EE20&\#x27; WITH \(TIMEOUT &\#x27;0.1s&\#x27;\) on the standby. The timeout is optional, and when supplied it raises an error if the replica does not catch up within the specified time.

rss · Simon Willison · Nov 19, 20:43

**「Background」** PostgreSQL major releases have usually arrived in September; this year&\#x27;s release came about two months later, which the source attributes mainly to the team&\#x27;s workload from a wave of AI-reported vulnerability reports. PostgreSQL standbys replay the primary&\#x27;s write-ahead log \(WAL\), and an LSN identifies a position in that log, so a standby can lag behind the primary until it has replayed through a given LSN.

**「Impact」** For applications that send reads to standbys, WAIT FOR LSN provides a built-in way to enforce read-your-writes per request: capture the LSN after a primary write, pass it to the standby, and optionally bound the wait with TIMEOUT so a lagging replica returns an error rather than stale data. This replaces hand-rolled replication-lag checks, but it requires the application to propagate LSN values between primary and standby sessions.

**Tags**: `#PostgreSQL`, `#database release`, `#WAIT FOR LSN`, `#WAL replication`, `#read consistency`

---

<a id="item-tech-news-2"></a>
### [Anthropic’s Nasdaq debut](https://www.reuters.com/business/finance/anthropics-historic-debut-put-ais-promise-peril-wall-st-test-2026-11-19/) ⭐️ 8.0/10

Anthropic made its Nasdaq debut on Nov. 19, 2026, Reuters reported, taking the AI developer into public markets. The supplied item includes no article body, so the offering size, IPO price, closing price, and valuation are not established by the source itself.

hackernews · wslh · Nov 19, 17:02 · [Discussion](https://news.ycombinator.com/item?id=50562754)

**「Background」** Anthropic’s Nasdaq debut is the first day its shares trade on a public exchange, following an initial public offering. An IPO sets an offer price, but the opening trade and closing price are set by public-market demand, so first-day moves are often reported against both benchmarks.

**「Community discussion」** Commenters treated the debut as both a valuation test and a career signal: one software engineer said the “gravy train” is over, while another noted the stock closed below its $111.50 opening trade but above its $83 IPO price. A programmer with 50 years of experience called it the sunset of this way of making a living, and the thread offered little consensus on what junior developers should do.

**Tags**: `#Anthropic`, `#AI industry`, `#IPO`, `#software engineering jobs`, `#valuations`

---

<a id="item-tech-news-3"></a>
### [PHP mixed-case HTTPS/FTPS schemes silently disabled TLS](https://x.com/ljachowicz/status/2123477025268924514) ⭐️ 8.0/10

PHP&\#x27;s HTTP/FTP stream wrappers recognized URL schemes case-insensitively but enabled TLS only when the fifth character was a lowercase &quot;s&quot;, so &quot;HTTPS://&quot;, &quot;httpS://&quot; and &quot;FTPS://&quot; were sent as plaintext, exposing tokens, Basic authentication, cookies, POST bodies and FTP login data, including after third-party redirects. The flaw is tracked as CVE-2026-128064 / GHSA-f6gg-rchx-xw8j with a CVSS 4.0 score of 8.2. It is fixed in PHP 8.2.36, 8.3.37, 8.4.28, 8.5.13 and 8.6.0; PHP 8.1 and earlier are EOL and will not receive a fix, so affected users must normalize URL schemes to lowercase.

telegram · zaihuapd · Nov 20, 03:04

**「How the scheme check worked」** PHP&\#x27;s HTTP and FTP stream wrappers recognize URL schemes case-insensitively, but they enabled TLS only when the scheme contained a lowercase &quot;s&quot; at a fixed position, according to the CVE description. PHP&\#x27;s 8.x changelog records the fix for GHSA-f6gg-rchx-xw8j under CVE-2026-128064, confirming that the selection logic was corrected in that branch.

**「Impact」** Applications on affected PHP versions that pass user-supplied or redirect-derived HTTPS/FTPS URLs to these wrappers remain exposed even when the code appears to use TLS; administrators should upgrade to a fixed release or lowercase the scheme before the stream wrapper processes it.

<details><summary>References</summary>
<ul>
<li><a href="https://everycve.com/CVE-2026-128064">CVE - 2026 - 128064 : Mixed-case HTTPS and FTPS URLs can expose...</a></li>
<li><a href="https://www.php.net/ChangeLog-8.php">PHP : PHP 8 ChangeLog</a></li>

</ul>
</details>

**Tags**: `#PHP`, `#TLS`, `#security vulnerability`, `#CVE`, `#web security`

---

<a id="item-tech-news-4"></a>
### [Anthropic claims Claude helped solve two black-hole physics problems](https://www.anthropic.com/research/claude-black-hole-physics) ⭐️ 7.0/10

Anthropic claims its Claude model contributed to solving two open theoretical problems in black-hole physics, in a company research post. The post is a vendor announcement, and the supplied material contains no independent verification or full paper details. A passage quoted in the comments says neither result describes our own universe directly and neither has practical applications, though both are presented as contributions to the long-running effort to reconcile quantum mechanics and relativity.

hackernews · cybermango · Nov 19, 17:30 · [Discussion](https://news.ycombinator.com/item?id=50563148)

**「Background」** Both results belong to the modular bootstrap, a program that uses mathematical consistency conditions on conformal field theories — in holographic duality, the boundary description dual to a gravitational bulk — to constrain which quantum theories of gravity are self-consistent. Because a black hole in the bulk corresponds to a thermal state of the boundary theory, a bound on black-hole mass at a fixed central charge becomes a test that any candidate theory must pass.

**「Practical scope」** Because Anthropic states that neither result describes our own universe directly or has practical applications, the near-term consequence is limited to specialists checking consistency conditions in candidate quantum-gravity theories, not a new experimental prediction or engineering method. Any follow-up would require independent verification of the derivations rather than treating the vendor announcement as an actionable result.

**「Community discussion」** Commenters debated how to characterize the result: one objected that “Claude solves” anthropomorphizes the model and noted that the word “prompt” does not appear in the blog post or either paper, while another described the second result as the more significant one—an upper mass limit consistent with a given central charge. Those are reader interpretations, not independent confirmation.

<details><summary>References</summary>
<ul>
<li><a href="https://www.anthropic.com/research/claude-black-hole-physics">Claude Fable 5.2 solves two open problems in the physics of black ...</a></li>
<li><a href="https://www.anthropic.com/research/claude-black-hole-physics">Claude Fable 5.2 solves two open problems in the physics of black ...</a></li>

</ul>
</details>

**Tags**: `#AI for science`, `#theoretical physics`, `#black holes`, `#Claude`, `#AI research`

---

<a id="item-tech-news-5"></a>
### [European Commission Deploys Matrix to 40,000+ Staff, Element Says](https://element.io/blog/how-the-european-commission-rolled-out-matrix-to-more-than-40-000-staff/) ⭐️ 7.0/10

Element&\#x27;s blog describes the European Commission&\#x27;s rollout of Matrix, an open-source federated messaging protocol, to more than 40,000 staff. The supplied material gives no client versions, encryption configuration, or independent assessment, so the scale is clear but the technical conditions are not.

hackernews · liotier · Nov 19, 10:58 · [Discussion](https://news.ycombinator.com/item?id=50558533)

**「Background」** Matrix is an open, federated messaging protocol, which allows an organization to operate its own homeserver while clients from different vendors connect to it. Element’s account says the Commission runs its own Matrix-based tool and integrated it with EU Login, and a report on the rollout dates the effort from a December 2025 prototype to completed laptop installation in September 2026.

**「Impact」** For other public-sector IT teams, the rollout is a 40,000-user reference for Matrix, but it does not by itself establish end-to-end encryption readiness or client compatibility; those teams would need separate evidence on encryption mode, session verification, and supported clients.

**「Community Discussion」** Commenters disagree sharply on readiness: one calls Matrix&\#x27;s encryption “a tire fire” and says the MLS migration appears abandoned, while a daily user cites fragmented clients, session verification, encryption errors, and slow development as persistent problems. Another commenter describes a small self-hosted friend group using Element X to avoid WhatsApp and Telegram, valuing private live-location sharing.

<details><summary>References</summary>
<ul>
<li><a href="https://element.io/blog/how-the-european-commission-rolled-out-matrix-to-more-than-40-000-staff/">How the European Commission rolled out Matrix to more than 40 , 000 ...</a></li>
<li><a href="https://dzen.ru/b/av7xwZrWnjnx2lAj">Еврокомиссия развернула Matrix на всех служебных... | Дзен</a></li>

</ul>
</details>

**Tags**: `#Matrix`, `#open source`, `#public sector`, `#end-to-end encryption`, `#enterprise deployment`

---

<a id="item-tech-news-6"></a>
### [OpenJDK &\#x27;java4shell&\#x27; PR debate centers on Oracle takeover and AI discovery](https://github.com/openjdk/jdk/pull/32781) ⭐️ 7.0/10

A purported “java4shell” OpenJDK vulnerability report, discussed in PR \#32781, remains unconfirmed in the supplied material: there is no official advisory, severity rating, or affected-version list. Commenters cite an Adoptium support issue in which the PR author said Oracle asked them not to proceed until approval and later said Oracle had taken over the report, and one notes Oracle&\#x27;s comment on a merged commit matches the PR wording. The thread also debates whether an LLM-assisted discovery independently found the issue or drew on an earlier public bug report.

hackernews · notmine1337 · Nov 19, 11:47 · [Discussion](https://news.ycombinator.com/item?id=50558906)

**「Background」** The OpenJDK flaw behind the &quot;java4shell&quot; label is tracked as CVE-2026-114938, which Cisco Talos rates at CVSS 4.0 9.2 and describes as a critical bug in Base64 decoding that can cause memory corruption, crashes and potentially unauthenticated remote code execution. The report surfaced as a pull request against the JDK repository rather than through a vendor advisory, and discussion points to an Adoptium support issue where, in early October, Oracle asked the author not to proceed with the PR until it granted approval, with the work described as &quot;taken over by Oracle&quot; by late October.

**「Who is exposed and what to do」** Security-vendor analyses of CVE-2026-114938 describe unauthenticated remote code execution through the OpenJDK Base64 decoder, affecting OpenJDK-based distributions built from 17.0.6 or later on x86-64 hosts with AVX-512 VBMI enabled. The practical mitigation is to move to a fixed build, and operators should first confirm whether their deployments run on AVX-512 VBMI-capable hardware, since the reported exploit path depends on those instructions.

**「Community Discussion」** Commenters split on provenance: one said an offline fuzzing harness found and exploited the issue independently before disclosure, while others argued an LLM could have seen the earlier Adoptium report or repository history. A shared caution was that judging criticality and constructing an exploit chain still needs human supervision even when AI assistance is plausible.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.talosintelligence.com/java4shell/">CVE-2026-114938: Critical vulnerability in OpenJDK Java</a></li>
<li><a href="https://socprime.com/blog/cve-2026-114938-java4shell-flaw-enables-pre-auth-rce-in-major-java-applications/">CVE-2026-114938: Java 4 Shell RCE Vulnerability</a></li>
<li><a href="https://orca.security/resources/research/java4shell-critical-openjdk-base64-decoder-flaw-could-allow-unauthenticated-remote-code-execution/">Java 4 Shell CVE-2026-114938: Affected Versions &amp; Mitigation</a></li>
<li><a href="https://blog.talosintelligence.com/java4shell/">CVE-2026-114938: Critical vulnerability in OpenJDK Java</a></li>
<li><a href="https://www.cyberkendra.com/2026/11/cve-2026-114938-pre-auth-rce-flaw-in-java-17-puts-servers-at-risk.html">Java 4 Shell (CVE-2026-114938): Affected Versions , Fix, Workaround</a></li>

</ul>
</details>

**Tags**: `#Java security`, `#OpenJDK`, `#vulnerability disclosure`, `#AI-assisted security research`

---

<a id="item-tech-news-7"></a>
### [UK government admits secret encryption order to Apple](https://macanorak.com/uk-government-forced-to-admit-it-issued-apple-a-secret-encryption-order/) ⭐️ 7.0/10

The UK government has admitted that it issued a secret encryption order to Apple, after being forced to disclose the order’s existence. The order is a technical capability notice, and its contents remain secret. The admission establishes that the UK pursued a covert demand against Apple, but it does not publicly show what technical changes, if any, were required or whether Apple complied.

hackernews · Terretta · Nov 19, 16:21 · [Discussion](https://news.ycombinator.com/item?id=50562113)

**「Background」** The dispute concerns the Home Secretary’s power to give a “relevant operator” a technical capability notice under section 253 of the Investigatory Powers Act 2016. An earlier Investigatory Powers Tribunal judgment, dated April 7, 2025, recorded extensive media reporting that the UK government had signed such a notice requiring Apple to keep users’ data accessible in decrypted form for intelligence agencies. The current judgment, Apple Inc v Home Secretary, was issued by the tribunal on November 19, 2026, and the government has now been forced to admit the order was issued.

**「Impact」** Apple users and enterprise security teams still cannot verify what the notice required or whether it affects the encryption guarantees Apple advertises, because the order’s contents are secret. That makes vendor security assurances harder to evaluate for UK deployments.

**「Community discussion」** Commenters focused on Apple’s security language: natch argued that Apple shifted from saying nobody, including Apple, can access user data to saying only that Apple itself cannot, and described a key-encryption-key layer that complicates the claim. fweimer pointed to the Investigatory Powers Tribunal judgment as the primary source and noted that the media learned of the notice through confidential security briefings rather than a leak; the order’s contents remain secret.

<details><summary>References</summary>
<ul>
<li><a href="https://investigatorypowerstribunal.org.uk/judgement/1-mr-vincent-kearney-2-british-broadcasting-corporation-v-1-chief-constable-of-the-police-service-of-northern-ireland-2-chief-constable-of-durham-constabulary-3-security-service-4-governme/">Apple Inc and Secretary of State for the Home Department and ...</a></li>
<li><a href="https://www.judiciary.uk/judgments/apple-inc-v-home-secretary-and-others/">Apple Inc -v- Home Secretary and others - Courts and ...</a></li>
<li><a href="https://investigatorypowerstribunal.org.uk/judgement/apple-inc-v-secretary-of-state-for-the-home-department/">Apple Inc v Secretary of State for the Home Department</a></li>

</ul>
</details>

**Tags**: `#encryption`, `#UK surveillance`, `#Apple`, `#privacy policy`, `#technical capability notice`

---

<a id="item-tech-news-8"></a>
### [PHP plans CRITICAL security release for supported versions](https://www.php.net/archive/2026.php) ⭐️ 7.0/10

PHP&\#x27;s security team says it will publish a security release on November 19, 2026, from 14:00 to 14:30 UTC to fix a vulnerability affecting all supported PHP versions, rated CRITICAL. The fix is part of PHP&\#x27;s regular four-week release cycle, and the team says the CRITICAL rating applies to an issue triggered only under non-default configurations or uncommon environments. Technical details and fixed version numbers are to be published with the release, so CVE identifiers and affected version ranges are not yet available.

telegram · zaihuapd · Nov 19, 07:10

**「为什么一次更新会涵盖所有版本」** PHP 并行维护多个受支持的发布分支，每个分支按各自的版本号接收修复，因此针对共享代码中缺陷的公告通常会同时为每个受支持版本发布一个更新。安全团队的提前通知惯例只宣布时间窗口和最高严重级别，实际细节和修复后的版本号则在发布时公布——这正是本次通知尚未提供的信息。

**「Impact」** Operators running any supported PHP branch should plan to upgrade after the release, but until the fixed version numbers and configuration details are published, they cannot determine whether their deployments meet the non-default conditions.

**Tags**: `#PHP`, `#security advisory`, `#critical vulnerability`, `#open-source software`

---

<a id="item-tech-news-9"></a>
### [OpenAI says models aided Jalapeño, AMD GPU design; AMD PPA up to 14%](https://openai.com/index/advancing-chip-design-with-our-models/) ⭐️ 7.0/10

OpenAI says its models contributed to the design of its Jalapeño inference chip and AMD&\#x27;s flagship GPU IP, and announced a Synopsys collaboration to train a GPT-Synopsys model. For Jalapeño, OpenAI reports roughly 13% lower standard-cell area in vector units and about 10% in matrix units, with the optimizations validated during chip bring-up. In the AMD work, OpenAI claims power, performance, and area improved by up to 14% over a highly optimized baseline, with some changes already in designs sent for manufacturing. All figures are OpenAI-reported and were not independently verified.

telegram · zaihuapd · Nov 19, 09:30

**「Background」** OpenAI&\#x27;s Jalapeño is a custom inference chip, and the Synopsys work builds on a partnership announced on September 30, 2026 to train a GPT-Synopsys model on Synopsys&\#x27; chip-design tools. That arrangement reportedly involves OpenAI paying Synopsys a training subscription plus revenue sharing once customers adopt the model and it demonstrably improves designs.

<details><summary>References</summary>
<ul>
<li><a href="https://yage.ai/share/ai-agent-pipelines-pricing-en-20261007.html">OpenAI Pays to Learn Chip Tools, an AI Agent Starts Emailing...</a></li>
<li><a href="https://www.taylortailored.co.uk/science-technology-1/openai-is-building-an-ai-that-designs-computer-chips-and-the-feedback-loop-could-be-enormous">OpenAI Chip Design: How The AI Feedback Loop... | Taylor Tailored</a></li>

</ul>
</details>

**Tags**: `#AI for chip design`, `#OpenAI`, `#AMD`, `#Synopsys`, `#semiconductor hardware`

---

<a id="item-tech-news-10"></a>
### [Gemini can now operate Macs for US subscribers, with background runs and pause controls](https://www.bloomberg.com/news/articles/2026-11-19/google-s-gemini-can-now-control-mac-devices-on-users-behalf) ⭐️ 7.0/10

Google&\#x27;s Gemini on Mac has gained a &quot;computer operation&quot; feature that clicks, types, browses menus and fills in forms on the user&\#x27;s behalf, according to a short secondary summary of the rollout. It is available to US users of the Mac Gemini app who subscribe to Google AI Plus, Pro or Ultra. Gemini runs in a separate background window while the user keeps using the main screen and cursor, and users can restrict which apps it may access, watch its actions in real time, pause it at any time, and approve key actions before they execute. The item cites no performance data, app-compatibility list, or independent verification of the capability.

telegram · zaihuapd · Nov 20, 02:51

**「Background」** Desktop-controlling AI agents work by driving a computer&\#x27;s graphical interface—clicking, typing, and navigating menus—rather than only responding in a chat window. Google is bringing this capability to Mac after rival assistants already offered comparable control, and early security coverage warns that granting an agent access to apps and files carries material risks.

**「Impact」** Because access is scoped per app and key steps need approval, subscribers delegating multi-step tasks will first have to define which applications Gemini may touch, and stay available to clear approval prompts; the summary does not say what happens when a task requires an app outside the permitted set or how failures are handled.

<details><summary>References</summary>
<ul>
<li><a href="https://www.bloomberg.com/news/articles/2026-11-19/google-s-gemini-can-now-control-mac-devices-on-users-behalf">Google’s Gemini Can Now Control Mac Devices on Users’ Behalf</a></li>
<li><a href="https://appleinsider.com/articles/26/11/19/gemini-can-now-control-mac-apps-but-you-still-shouldnt-let-it">Gemini can now control Mac apps, but you shouldn&#x27;t let it</a></li>

</ul>
</details>

**Tags**: `#AI agents`, `#Google Gemini`, `#desktop automation`, `#macOS`, `#user controls`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Asian stocks fall as doubts about AI spending grow after Anthropic IPO](https://www.bloomberg.com/news/articles/2026-11-19/stock-market-today-dow-s-p-live-updates) ⭐️ 8.0/10

Anthropic shares fell more than 5% in after-hours trading to below $92, and Asian equities dropped broadly as investors questioned whether heavy AI spending will deliver returns. The MSCI Asia-Pacific index fell 1.7% for a seventh straight session, while South Korea&\#x27;s Kospi fell 3.66%, with SK Hynix down 6% and Samsung Electronics down 4.7%.

telegram · zaihuapd · Nov 20, 01:58

**「Background」** Anthropic’s initial public offering had been billed as a make-or-break test for the AI trade and was reportedly six times oversubscribed ahead of the listing, so its post-IPO decline became a signal for broader AI valuations.

<details><summary>References</summary>
<ul>
<li><a href="https://www.marketpulse.com/markets/anthropics-ipo-a-make-or-break-test-for-the-trillion-dollar-ai-trade/">Anthropic’s IPO: A make-or-break test for the trillion-dollar ...</a></li>

</ul>
</details>

**Tags**: `#AI investment`, `#Asian equities`, `#semiconductor stocks`, `#market selloff`, `#SoftBank/OpenAI`

---