---
title: "Writing for Impact: Revisions"
authors:
 - arj
date: 2024-08-13 11:30:00 -0500
summary: "Sharpen your writing by removing filler and jargon, and by “activating” your prose."
image: /images/writer.jpg
tags:
  - cybersecurity
  - writing
math: false
---
{{< figure src="/images/writer.jpg" title="Writer at work." >}}

_Note: This post is the fourth in a series of excerpts from a style guide I wrote in 2021 when I was the CISO and General Manager of QOMPLX, a visionary but now-defunct security services vendor. Its internal title was “Writing for Impact: Ridding Yourself of Habits that Cause Your Written Communications with Clients and Colleagues to Suck.” The primary targets for the guide were consultants on our professional services team. I am publishing it here, minimally edited, as a service to the cybersecurity community, which has been so generous to me over the years._

The preceding posts in this series describe how to create effective document types. They provide the skeletal structure for our written deliverables. In this post, we turn to style—the muscle.

# The Good, the Bad and the Ugly
As a former English teacher explained to me once, “Revision means _re_-vision”. We become better writers by seeing our words in a new light. Conscientious editors and peer reviewers can help. So can good examples. The sections below offer examples of writing that have been improved before (the “Bad and Ugly”) and after editing (the “Good”). The “Why” column explains how each revision improves on the original.

# Eliminating filler
When writing an technical document, you may be tempted to fill your page with jargon, stock phrases, and dependent clauses that might mean something to you, but don’t mean much to the reader. Too many words dilute meaning, and cumulatively yield a whole lot of nothing. These examples demonstrate how to get your point across more directly.

<table>
  <thead>
    <tr>
      <th width="33%">Bad and Ugly</th>
      <th width="33%">Good</th>
      <th width="33%">Ugly</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>The main things that QOMPLX often finds customers not giving enough attention are oversubscribed key team members, OS versions (mainly Domain Controller OS versions and functional levels) are not at the latest available versions, Active Directory backups are not being copied or sent to immutable storage, Forest Recovery exercises are not being done on an annual basis (or sooner), weak Default Password Security Policies, minimal use of Fine-grained Password policies, lots of stale user and computer accounts, and measures to block the ransomware threats (i.e., deploying/upgrading-to modern Windows OSes with Controlled Folder Access, File Servers with FSRM and Anti-ransomware or file whitelist policies, and the use of immutable storage for backups) are frequently overlooked.</td>
      <td>Active Directory is an aging technology that is complex to operate. Many organizations do not keep Domain Controller operating systems current and patched. Others do not implement effective policies that enforce strong passwords, protect filesystems, or provide fine-grained security. Overworked teams do not consistently implement controls that would reduce the impact of ransomware, such as tabletop drills, immutable server backups, and recovery testing.</td>
      <td>The original sentence in the source document spanned eight full lines of text. It needed a starvation diet. Readers care less about the actual technical details than the themes: keeping stuff current, maintaining good policies, and operating the plant effectively. As an improvement, we grouped the basic points into three chunks and summarized the details of each chunk. We simplified “oversubscribed team members” (walking magazines?) to “overworked teams.” And we started off by making the essential point: this stuff is <em>hard</em>.</td>
    </tr>
    <tr>
      <td>As shown in the questions and answers section of this paper, there does exist a subset of the required components that would make up a fully functional security operations activity. The following section will describe areas that require improvement and observations.</td>
      <td>To detect and respond to cyber threats, organizations need a core set of operational capabilities. Fresh Retail possesses some of these. This section describes necessary capabilities, and recommends improvements.</td>
      <td>“There does exist a subset of the required components that would make up” is a word salad. Change the order of ideas to establish principles first: “ya gotta have some basic stuff in place. Some of it ya got, some ya don’t. Read on for more details.”</td>
    </tr>
    <tr>
      <td>The CIS Security Control Framework is an effective security control framework for any organization to use in conjunction with other security tools and software as it also provides benchmarks for self evaluation to the standards.</td>
      <td>Organizations use CIS Controls to benchmark their security processes, tools, and software.</td>
      <td>In addition to being 35 words long, this sentence also contains six prepositional phrases that make it very hard to follow (“for any,” “to use” “in conjunction” “with other,” “for self” and “to the”). The “in conjunction with” phrase is just duct tape that says nothing at all. “As it also“ means “because” in this context, but is unnecessary in the revision. You can whack two-thirds of the words without losing essential meaning. Note the Oxford comma (between "tools" and "and software"), which Benjamin Dreyer and other noted editors recommend using to avoid ambiguity. (Dreyer would have you believe that <a href="https://www.theguardian.com/books/2019/may/30/dreyers-english-by-benjamin-dreyer-utterly-correct-guide-to-clarity-and-style">“only godless savages” omit the Oxford comma.</a>)</td>
    </tr>
  </tbody>
</table>

# Activating Your prose
Passive voice is the curse of the thinking classes. We technical folk believe that lots of “it is understood that”s and “was performed”s lend an air of white-coated, clinical objectivity to our prose. In fact, passive voice obscures agency. Readers cannot know _who_ imparted the magical knowledge that resulted in our understanding, or _who_ performed the fabulous action worth mentioning. Abusers of passive voice mislead readers. The following examples show how actively-voiced sentences clarify responsibilities and recommendations.

<table>
  <thead>
    <tr>
      <th width="33%">Bad and Ugly</th>
      <th width="33%">Good</th>
      <th width="33%">Ugly</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>The methodology of this engagement was limited by Fresh Retail to a vulnerability assessment of specific internal retail store network ranges.</td>
      <td>Fresh Retail limited the scope of the assessment to internal retail store ranges.</td>
      <td>Remove passive voice to clarify the subject (Fresh Retail did the asking, and imposed the limits), rather than surprise the reader later.</td>
    </tr>
    <tr>
      <td>It is understood that Fresh has deployed the Trend Micro anti-virus agent&hellip;</td>
      <td>Fresh deployed Trend Micro anti-virus agents&hellip;</td>
      <td>Why weasel out of a simple factual statement with “It is understood that&hellip;”? If we’re not sure, verify with the client—or cut the phrase.</td>
    </tr>
    <tr>
      <td>Ensuring a seamless authentication experience for users is imperative.</td>
      <td>Ensure a seamless authentication experience.</td>
      <td>If you end a sentence with “&hellip;is an imperative” (a command), why not just write it in an imperative voice?</td>
    </tr>
  </tbody>
</table>

# Excising jargon
Security and risk experts love words that the rest of the population find weird or impenetrable: _exfiltrate_, _remediation_, _nonrepudiation_,[^1] and _zero-day_, to name a few. We might say “exfiltrate” when we could more usefully say “steal,” or “data loss” when “theft” would be less obscure. In-group jargon confuses aunts and executives alike. The following examples demonstrate how to improve your prose by excising stupid stuff normal people don't say.

<table>
  <thead>
    <tr>
      <th width="33%">Bad and Ugly</th>
      <th width="33%">Good</th>
      <th width="33%">Ugly</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>While there is a level of log management capability in the Trend management interface, the resultant logs are not being aggregated into the SIEM for correlation and monitoring purposes. While these logs would provide coverage to Fresh for the anti-virus and possibly anti-spyware occurrences, there is a facility for capturing process level information, however.</td>
      <td>Trend Micro logs virus and spyware activities on endpoints. However, these logs are not sent to the SIEM for additional correlation and analysis. Fresh has not enabled process-level logging, which would capture evidence of malicious activities. Without the additional context gained from endpoints, Fresh Retail may not be able to detect attacks in progress.</td>
      <td>“There is a level of log management capability” is wholly empty of meaning. “Resultant logs” is gibberish. The point of this sentence is that Trend’s data hasn’t combined its endpoint logs with other SIEM data, which means they have a blind spot. To re-write, state the facts: “Trend collects this, but not that. Logs don’t go to the SIEM, etc. Here’s why that’s bad.” (Speculation is ok here.)</td>
    </tr>
    <tr>
      <td>High risk findings that could provide a path to exfiltration of sensitive data and total system compromise include:</td>
      <td>High-risk vulnerabilities that could allow an attacker to completely compromise Fresh’s systems or steal data include:</td>
      <td>“Provide a path to exfiltration” is too indirect and full of jargon. “Allow an attacker to&hellip; compromise&hellip; and steal&hellip;” orders the ideas better (compromise first, then steal&hellip;) and is clearer. “Findings” is neutral;“vulnerabilities” is more precise, and provides the negative tone we want. Note: “High-risk” should also be hyphenated, because these two words modify a noun (“findings”).</td>
    </tr>
    <tr>
      <td>Retain security logs for as long as possible or for a prescribed time frame required according to presiding policy or governance.</td>
      <td>Create a policy for retaining logs, as required by regulations, statutes and contracts. Implement the policy.</td>
      <td>Lots of gerunds and some foolishness: policies can’t preside, and governance can’t either. Split the sentence into two complete thoughts: “you need a policy; and then, you need to implement it.”</td>
    </tr>
  </tbody>
</table>

# Fine points
In prose as with certain outdoor sports, “close only counts in horseshoes and hand grenades.” We all benefit from revisions, including on fine points of grammar or clarity. The following examples demonstrate incremental improvements that make the reader’s job just a little bit easier. 

<table>
  <thead>
    <tr>
      <th width="33%">Bad and Ugly</th>
      <th width="33%">Good</th>
      <th width="33%">Ugly</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Fresh Retail Company (Fresh Retail or Fresh) engaged QOMPLX, Inc. (QOMPLX) in March of 2020 in order to assist them in better understanding the security posture of their retail store environments.</td>
      <td>Fresh Retail Company (“Fresh Retail” or “Fresh”) engaged QOMPLX, Inc. (“QOMPLX”) in March of 2020 to assess the security posture of its retail store environments.</td>
      <td>The phrase “in order to assist them in better understanding” has three preposition phrases in a row (“in order”, “to assist” and “in understanding”). You can simplify to “to assess” without any loss in meaning. Note: “their” is inappropriate when referring to a corporate entity; always use “its.”</td>
    </tr>
    <tr>
      <td>These high-risk findings reflect the fact that Fresh Retail does not have an effective threat and vulnerability management program established.</td>
      <td>These high-risk findings suggest that Fresh Retail’s vulnerability management program is not effective.</td>
      <td>It is <em>not</em> a “fact” that Fresh’s program is ineffective, only our opinion; the revised “suggest” indicates that clearly. “Threat and&hellip;” is not exactly redundant but adds no value here, so snip it.</td>
    </tr>
    <tr>
      <td>Even with this limitation QOMPLX determined that the weaknesses and vulnerabilities discovered in the engagement would allow a hostile attacker the ability to negatively impact Fresh’s operations.</td>
      <td>Despite this limitation, QOMPLX determined that attackers could exploit these weaknesses to disrupt Fresh’s operations.</td>
      <td>“Negatively impact” means nothing, because “impact” means “affect,” and “affect” is neutral. Why not say what the effect is, rather than beat around the bush? “Despite” is a better choice than “even with.” Note the comma after “limitation.”</td>
    </tr>
    <tr>
      <td>Disable any services or applications which is not required by operational needs.</td>
      <td>Disable all unnecessary services and applications.</td>
      <td>The phrase “which is not required&hellip; by needs” can be more simply replaced by “unnecessary.” Snip “by operational needs” because it adds nothing to the meaning; it is filler.</td>
    </tr>
  </tbody>
</table>

_In the last post in this series, I’ll close with some advice about words and phrases to avoid, and what to use in their places._

[^1]: I dislike all of these words because they are fundamentally in-group, cool-kid words that nobody outside of the the cybersecurity community understands. But I reserve special disdain for _nonrepudiation_, which was wholly invented in the mid 1980s by cryptographers in lawyers’ drag. The idea was that cryptopgraphic digital signatures would provide incontrovertible proof that someone who signed a thing, digitally, really did sign in. Because of the magic of cryptography, so the theory went, the signer could not “repudiate” their digital signature. Digital signatures really _are_ awesome because they provide tamper evidence. And the stuff that derives from digital signatures, such as blockchain, are more awesome still. But the notion that multiplying two massively long prime numbers together somehow overturns 500 years of contract law is just silly. If you need further proof (see what I did there&hellip;), you will find that nonrepudiation [does not appear in publications, law journals, or case law prior to 1985](https://books.google.com/ngrams/graph?content=nonrepudiation&year_start=1800&year_end=2022&corpus=en&smoothing=3). Plus, people “repudiate” stuff all the time. Like [when their Bitcoin wallets](https://www.investopedia.com/articles/investing/032615/can-bitcoin-be-hacked.asp) are stolen. Flame off.