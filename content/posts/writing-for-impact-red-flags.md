---
title: "Writing for Impact: Red Flags Documents"
authors:
 - arj
date: 2024-08-12 11:30:00 -0500
summary: "Corporate acquirers want to know whether they are buying firms with cyber problems. Red Flags letters identify trouble spots, question marks, and investment areas."
image: /images/writer.jpg
tags:
  - cybersecurity
  - writing
---
{{< figure src="/images/writer.jpg" title="Writer at work." >}}

_Note: This post is the third in a series of excerpts from a style guide I wrote in 2021 when I was the CISO and General Manager of QOMPLX, a visionary but now-defunct security services vendor. Its internal title was “Writing for Impact: Ridding Yourself of Habits that Cause Your Written Communications with Clients and Colleagues to Suck.” The primary targets for the guide were consultants on our professional services team. I am publishing it here, minimally edited, as a service to the cybersecurity community, which has been so generous to me over the years._

A _Red Flags_ document, or as it is formally known, a “Summary of Engagement” document, describes what a client needs to know about a company they are planning to acquire. Red Flags engagements generally include the following activities:

- An external vulnerability scan and open-source intelligence review, including known cyber breaches, social media exposure, data leaks and external cyber hygiene deficiencies
- “Desk research” about the company
- Review of security policies and standards

The Red Flags document should be three to four pages maximum. Red Flags documents are different from the _Executive Summary_ of an assessment-style deliverable. The combination of a fast delivery cadence and an arm’s-length relationship with the target means that our conclusions will be necessarily incomplete, and more tentative. But we need not mince words, either. The sections that follow describe how to write the document, which includes an _Introduction_, _Observations_, _Discussion_ and _Areas for Additional Inquiry_.

# Introduction
The _Introduction_ describes how we were engaged, and the context of the deal. It also says what we did to assess the cybersecurity posture of the target, in plain language. Where appropriate, it includes factoids that characterize the effort. For example:

> Abacus Equity engaged QOMPLX to understand the cyber and operational risks of Papermasters, a company that it is evaluating for a strategic acquisition. Papermasters provides outsourced business services for enterprises in the areas of benefits administration and wealth management. QOMPLX’s pursued four lines of inquiry. During the engagement, QOMPLX:
>
> - Performed an __open-source intelligence assessment of risks__ to Papermasters and related subsidiaries, based on publicly available information, deep- and dark-web analysis, and other methods
> - Reviewed __historical breach data__ and related commentary provided by management and in the public domain
> - Assessed the __external security posture__ of Papermasters and related subsidiaries, using vulnerability scanning tools and manual assessment techniques
> - Reviewed over 300 __documents supplied by Papermasters management__ related to its technology footprint, roadmap, security program, material agreements, vendor contracts, and legal obligations
>
> Our engagement started on December 4th, 2020 and is continuing as of this writing on December 18, 2020. Several requests for information with Papermasters are still pending at time of publication for this draft of key findings.
> All identified issues can be remedied with sufficient investment and executive involvement. We recommend that detailed modernization and improvement actions should be an explicit part of post transaction planning and financial analysis. Planning efforts should focus on modernization and improvements to security tools and infrastructure. By streamlining its technology stack, Papermasters can also reduce ongoing operational costs compared to historical levels of spend.

# Observations
The _Observations_ section includes four to eight “long bullets” that provide thematic impressions of risks we can see from our work. The language should communicate firm impressions but leave room for uncertainty. The overall length of this section should be approximately one page. The language should be non-technical and written in clear, concise, active-voiced prose, without acronyms or jargon. Do not obscure impressions if they are firmly held. Include relevant factoids where possible. Move all technical detail or side commentary to footnotes; a bit of sly wit in a footnote is ok, but informal language is not. Do not include recommendations or speculate about future uplifts in the _Observations_ section; keep commentary focused on facts and impressions.

For example:

> All security and risk diligence assessments have intrinsic limitations. QOMPLX’s ability to form conclusions are necessarily limited by the time allotted, depth of analysis, degree of cooperation by the target and other factors. QOMPLX observed five main themes in its review:
> - __Papermasters’ technology platforms are highly fragmented__, and that pattern is likely reflected in the company’s internal efforts. We observe fragmentation in our external security reviews as well as our review of technology and security documents provided by management. Papermasters is attempting to fix this problem through its Paper Plane technology roadmap, which will transition the company away from older on-premises solutions towards cloud-based services. At present, Paper Plane appears to be a collection of buzzwords and unrelated technologies that read less like a coherent, curated roadmap and more like a laundry list of regional favorite technologies that have not been fully de-conflicted or intentionally designed as part of a coherent system of systems.<sup>1</sup>
> - __Papermasters appears to be “well-papered” from a security policy standpoint__. The number and kind of security policies cover the topics they should. The capstone Global Information Security Policy is well-written, and references 16 subsidiary standards which are generally well-done. But the top-level Policy is only two years old; it was written by E&Y, rather than in-house, and lacks operational contextualization or nuance given the extensive outsourcing used in practice. Moreover, policies and standards appear to be cherry-picked from different parts of the organization—some from the legacy Cedar organization, and some from Papermasters proper with inconsistent application. We noted thin coverage in several areas, notably, a superficial treatment of privacy matters in the incident response plans for the Incident Response Center (IRC), and limited procedures and technology investments in application security. Business resilience, by contrast, appears to be one area that is both well-papered and well-practiced.<sup>2</sup>
> - __Papermasters prefers outsourcing security and risk management services to running them themselves__ with an insourced security team. We noted its outsourcing of security monitoring services, for example to Blue Voyant for firewall management, and to Kroll for security incident first response. Some strategic third parties, such as Accenture, have experienced major system compromise and data breaches, which may in turn expose Papermasters to such risks. Papermasters appears to have no security vendors with which it spends more than $1 million annually. Federated programs which are of this nature are typically very difficult to fully command and control in the event of a major incident.
> - __Papermasters has a history of prior, serious, data breaches__. In 2017, Papermasters provided notice of data breach to their consumers. A five-year-long breach was discovered in a “routine” FFIEC exam, a surprisingly substantial disclosure that implies serious operational security gaps which persisted for a prolonged period. Papermasters’ prior CISO left the company seven months ago and was succeeded by an incumbent manager. The new CISO articulated some positive directional change aspirations during the diligence call but additional clarity regarding management sponsorship, authority and planned investment is paramount.
> - __We noted many Indicators of continuing security operational gaps__ in our scans of Papermasters’ external perimeter. Observed conditions include vulnerable websites, servers, firewalls, VOIP services, and web applications due to patch management deficiencies. A few of these are serious and should be fixed immediately. We’ve described these findings in detail in a separate Intelligence Assessment deliverable. External fingerprinting identified a particularly memorable example in one of Papermasters’ major products, which uses an almost ten-year-old version of PHP in an application. That product runs inside an enterprise application portal built on technology that is fifteen years old. We found a very large number of sites operated by Papermasters which don’t employ modern security practices (such as secure cookies) as part of its normal software development lifecycle.
>
> <small><sup>1</sup> For example, the Four Pillars freely intermix 40 similar and different technologies including Java, .NET, Azure, AWS, Docker, IBM, EMC, CloudEra, Spring, Tableau and Verint. Its Analytics and BI materials mention every tool made since the beginning of time in seemingly every area of IT, ranging from Novell to Alteryx, R, Spark, Cloudera, DB2 and New Relic.</small>
>
> <small><sup>2</sup> Documentation of disaster recovery processes are complete and thorough. Papermasters uses an outside SaaS package for business continuity planning. Papermasters takes an asset-, application- and data-center centric approach to DR exercises. This is appropriate; however, financial regulators increasingly expect a business process-centric strategy for testing.</small>

# Discussion
After noting our key observations, discuss the risks related to the acquisition. These should convey what the acquirer will need to fix or invest in. Speculate—and reserve the right to be wrong—about areas of exposure; use “appears” to convey uncertainty judiciously and where warranted. Write discussion points as long bullets, one theme per bullet. Add facts and data to back up your points. Highlight the key thought in each bullet in boldface, so that it is easy to spot. For example:

> - Given its existing external exposures, it is almost certain that Papermasters is currently experiencing __automated, and probably human-directed, attack attempts by threat actors__. This can be confirmed by examining security logs, although it is not clear that Papermasters’ logging is comprehensive enough.
> - __Application security is an area of likely risk__. Papermasters’ Agile methodologies are well-described and thorough. But evidence of SDLC integration appears limited to policy requirements. Training appears limited. In its list of key technology initiatives totalling approximately $50 million in planned spending—the largest of which appear to focus on hyper-personalization and data convergence across entities—security or fraud initiatives are missing. Over 300 externally facing websites appear to have substandard encryption, and we found expired TLS certificates.
> - __Legacy infrastructure carries significant risk__. Papermasters’ infrastructure is a mix of legacy and modern cloud systems. QOMPLX found that most serious technical vulnerabilities were in older systems, many of which are unsupported or unpatched but still part of the company’s infrastructure. Documents we reviewed lack clarity about modernization implementation plans or resourcing. Substantial investment should be made.
> - We do not yet understand __Papermasters’s degree of control effectiveness__. QOMPLX reviewed a small number of third-party assurance reports such as the SOC 2/HITRUST Assessment, which turned up a few gaps related to developer access in production, account removal processes, and Unix password compliance. These may or may not be concerning. To form more definitive conclusions, QOMPLX would like to see artifacts related to identified vulnerabilities and risks, as well as, for example, IT General Controls testing reports for Sarbanes-Oxley. These additional RFIs are pending.
> - Our observations about operational security gaps, legacy infrastructure exposures and SDLC concerns indicate that __Papermasters has not incorporated security into its culture__. Security is most likely seen as an “IT issue” instead of a business risk management issue. We did not see evidence of a strong risk oversight program within the company, but our impressions may be incorrect pending additional information.
> - Beyond security risk, Papermasters is in the midst of a __technology transformation program__. Many of its key applications, such as Pulp 2.0, are based on technologies that are ten-to-twenty years old and need to be refreshed. The efforts to modernize its platforms are commendable and necessary, but carry with them significant execution and operational risks.

# Areas for Additional Inquiry
The _Observations_ and _Discussion_ sections describe our impressions of the target, and where we believe it may need to invest time, money and resources. But our impressions are necessarily incomplete. If we believe we can gain additional clarity by reviewing additional information, use the _Areas for Additional Inquiry_ section to ask for what we want. For example:

> In light of its history of prior security incidents and to identify additional risk themes, QOMPLX has requested the following additional information from Papermasters:
> - _Penetration test results_ since Jan 2019
> - _Significant security Incidents_ (that is, those reported to a management committee) since Jan
2019; if available, include recent incidents & lessons learned
> - _Significant risk acceptances or control exceptions_ registered since Jan 2019
> - _Security vulnerabilities_ identified by the Vuln Management program, since Jan 2019
> - _Security organization chart_, as of December 2020, including embedded resources outside of
the center
> - _Notable internal audit findings_ related to cyber & operational risk since Jan 2019
> - _Cyber and operational insurance claims_ filed since Jan 2019
> - _Sarbanes-Oxley Section 404 IT General Controls external audits_ since January 2020; notably, any qualifications from last 3 quarterly audit periods

# Wrapping Up
A Red Flags document summarizes expert opinion about the security posture of a corporate target for acquisition. These documents are necessarily speculative because they do not have the rigor of a full-blown assessment and must be done quickly. A Deloitte ITGC auditor or Second Line of Defense risk officer would blanch at the speed and seeming lack of precision in a typical Red Flags analysis. But the comparative lack of depth and rigor is not, in the eyes of a corporate acquirer, a significant deficiency. Indeed, when performed by a small, sufficiently seasoned team, Red Flag documents can be accurate without being precise. They give the acquirer a good idea of where they are likely to need to allocate funds post-acquisition. Acquirers can also choose to use rough cleanup cost estimates as part of the deal consideration prior to closure.

_In the next post in this series, I’ll show you real-life examples of prose that benefited from edits, with “before” and “after” versions side-by-side. With apologies to Sergio Leone, this post will be “[The Good, the Bad, and the Ugly](https://www.youtube.com/watch?v=Gjq0w-tzVg4).”_
