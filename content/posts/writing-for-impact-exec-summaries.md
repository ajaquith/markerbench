---
title: "Writing for Impact: Executive Summaries"
authors:
 - arj
date: 2024-07-31 21:30:00 -0500
summary: "The Executive Summary is your first—and often last—chance to persuade decision-makers. Here’s how to stick the landing."
image: /images/writer.jpg
tags:
  - cybersecurity
  - writing
featured: true
---
{{< figure src="/images/writer.jpg" title="Writer at work." >}}

_Note: This post is the second in a series of excerpts from a style guide I wrote in 2021 when I was the CISO and General Manager of QOMPLX, a visionary but now-defunct security services vendor. Its internal title was “Writing for Impact: Ridding Yourself of Habits that Cause Your Written Communications with Clients and Colleagues to Suck.” The primary targets for the guide were consultants on our professional services team. I am publishing it here, minimally edited, as a service to the cybersecurity community, which has been so generous to me over the years._

QOMPLX is an opinionated company. We believe that all companies deserve our products and services. We hold these truths to be self-evident. But our clients may not agree they are quite so evident. That is why we write documents during our engagements—to memorialize our work, state risks plainly, and recommend actions our clients should take. When we do this well, we win more business. When we don’t, our clients scratch their heads and wonder what the point of hiring us was.

QOMPLX’s core documents are generally _assessments_, which render opinions about risk topics important to our clients. Three important types of assessments include:

- __Critical infrastructure assessments__, which combine Q:SCAN and vulnerability-scanner data to identify vulnerabilities and exposures in their external presence and Active Directory infrastructure that attackers can exploit.
- __Intelligence assessments__, which use open-source intelligence to create a dossier of risks that can be gleaned from a variety of sources.
- __Red Flags letters__, which tell potential acquirers of companies what they need to know about their targets’ security weaknesses.

# Key Sections
Typical assessment-style documents contain four sections:

- The __Executive Summary__ introduces the engagement and summarizes the essential information our executive sponsors need to know. Subsections include the _Introduction_, _Background_ (optional), _Key Findings_, _Recommendations_, and _Actions Already Taken_ (optional).
- The __Objectives and Process__ section describes how we did our work, and who did it. Subsections include the _Work Plan_, _Scope_, and _Team Members_.
- The __Findings__ section lists the issues we found, and describes them in detail. Subsections include the _Summary of Findings_ (a table); and _Findings in Detail_, with each finding listed in descending order by severity.
- The __Appendices__ contain tool output, screenshots, log output and supporting documentation.

Of these sections, the _Executive Summary_ is of paramount importance, because it is our first—and often last—chance to make an impression on our readers.

# How to write an Executive Summary
The _Executive Summary_ is the most important part of any engagement deliverable, because it is the portion of the document that will be discussed first, and circulated upwards. As with public speaking, it is essential to have a “high-impact opening,” and as with gymnastics, to “stick the landing.” That’s because it is _for executives_. That means making every word count.

A good Executive Summary does not mince words, and leaves no ambiguity unless we wish to qualify statements for a specific reason. Let’s review the components of a typical Executive Summary: the _Introduction_, _Background_ (optional); _Key Findings_, and _Recommendations_.

## Introduction
The first section—not more than two paragraphs—describes what the client wanted when they engaged us. It then lists a few salient facts, such as when the engagement started and ended, and what we did. Everything in the _Introduction_ should be 100% factual. In some cases, you may add an opinion-laden “zinger” to the end. Here are two examples of an _Introduction_:

> Fresh Retail Company (“Fresh Retail” or “Fresh”) engaged QOMPLX, Inc. (“QOMPLX”) in November of 2020 to assess the security posture of a small subset of their retail store environments. This limited engagement is the initial phase of discovery, and is part of a larger effort to understand Fresh’s ability to protect and defend itself against malicious attackers. Our assessment focused on Fresh’s authentication and authorization controls, types and flows of data, network architecture, logging, and other indicators of its security posture. QOMPLX believes Fresh Retail is a target of choice because of its vast size and presence, with 200 stores serving 120 million customers.[^1]

and:

> In December 2020, Construx engaged QOMPLX to assess its compliance with the NIST 800-171 standard for protecting unclassified information, as required by US federal contracting guidelines. Working with Construx staff, QOMPLX assessed the firm’s controls and is currently working with Construx on the best approach for reporting the results to the US federal government’s Supplier Performance Risk System (SPRS) system. The engagement began after the November 2020 deadline for filing, and concluded in January 2021.

These examples are “all business”—no fluff, no wasted words. Note the use of active voice in most of the sentences: “Fresh Retail _engaged_ QOMPLX.” “Our assessment _focused on_&hellip;,” and “The engagement _began_&hellip;”

## Background (optional)
Occasionally, readers may need additional information that provides valuable context about the engagement. Background sections should be short, not more than two or three paragraphs at most. For example, a CMMC assessment probably needs a brief discussion of what CMMC is, and why the client needs accreditation to pursue government business. Here’s an example:

> On September 2020, the US Department of Defense changed its guidelines for awarding contracts. The DoD now requires contractors to have filed compliance scores in SPRS, based on self-assessments against the NIST 800-171 standard. In order to do that, contractors must have also filed System Security Plans (SSPs), which are multi-hundred-page documents that describe security programs in detail. Prior to December 2020, Construx had done neither of these things.
>
> To preserve its DoD business, Construx needed to file in SPRS as quickly as possible. Construx agreed to self-assess as if the SSP did exist. QOMPLX assisted Construx with its NIST 800-171 self-assessment and is coordinating with Construx on the best approach for filing the resultant score in SPRS. QOMPLX subsequently assessed the remaining 20 CMMC Level 3 controls. The assessment’s scope included all people, systems, and business entities in Construx.

In this example, we set the context for the _Key Findings_ that follow. This is an important context to have, because it conveys the urgency of the work we have done for the client.

## Key Findings
Of the time you spend writing the _Executive Summary_, spend at least one-third of it nailing the _Key Findings_. This section recaps the most important issues we found, and it should be chock-full of our observations. _Key Findings_ are meant to get the attention of executives.

The smarter executives—the ones that shell out real money to solve big problems—were not born in the woods. They want detail. They want facts. If we burble on about how they “don’t have control of their inventory” or “have significant cyber exposures” or “have a large number of unpatched systems” without describing why we believe what we wrote, we lose credibility. When we make general statements without backing them up with specifics or data, we give clients reasons to discount our insights and advice.

As an author, your goal is to avoid FOG—“fact-deficient, obscuring generalities.” A well-constructed _Key Findings_ section cuts through the FOG. It begins with a discussion of what we found at a high level, including a firm statement about the business consequences. It then discusses four-to-eight of the most important findings, as bullets. Generally, these will be “Critical” or “High” issues mentioned in the more detailed _Findings_ section of the document. They may also describe thematic issues that span multiple findings.

You may choose to write _short bullets_ of one or two sentences each, not more than about three lines of text. You can also write _long bullets_ that run to four-to-six lines, with a boldfaced key phrase. Choose a format and stick to it. Whichever style you choose, make firm statements without qualification whenever possible, back them up with facts, and state the business consequences. Always answer “What It Means.”

### Short bullets
Short bullets are appropriate in shorter Executive Summaries. Here’s an example of a “short bullet” style, which includes a brief introductory paragraph followed by several short bullets.

> Fresh Retail asked QOMPLX to limit its vulnerability assessment to specific internal retail store ranges. QOMPLX did not exploit any vulnerabilities we found. Nonetheless, QOMPLX determined that weaknesses discovered during the engagement would allow a hostile attacker to disrupt Fresh’s operations. Critical and high-risk vulnerabilities that could allow an attacker to compromise Fresh’s systems or steal data include:
> - One server can be easily exploited by the four-year-old ETERNALBLUE vulnerability, allowing the internal network to become victim to a mass ransomware attack.
> -  A terminal server permitted unauthenticated access to sensitive functions including video security monitors.
> - Twelve hosts running unsupported Windows operating systems with several critical vulnerabilities. These systems cannot be patched because they no longer receive vendor security updates from the manufacturer.

Note the specificity in each of these points. All of them benefited from edits. For example, before edits, the first bullet read “Indicators that a server used by Fresh Retail stores is vulnerable to a ransomware attack via a well known, easily exploited vulnerability.” That’s actually not too bad, but a bit of editing made it a lot harder hitting:

- We changed the vague “Indicators&hellip;” and “a well-known, easily exploited vulnerability” to the specific ETERNALBLUE and noted that it is four-years old!
- Sharpened the “vulnerable to a ransomware attack” phrase to “allowing the internal network to become victim to a mass ransomware attack.”
- Changed “a server” to “One server” and started the bullet with that phrase, rather than burying it later in the sentence.

These changes make the bullet far more memorable. _Holy crap, I’ve got a four year vuln on my network that a bad guy could use to start a four-alarm fire! And it’s ETERNALBLUE, that thing I read about in the papers!_

One more example. The second bullet originally read “Physical security systems are configured for unauthenticated remote access.” This is all true and accurate. But when we read the _Findings_ detail, we find a nice-looking screenshot that shows retail store cameras. But wait, there’s more! It’s a VNC server—and no password is needed. So for this one, we made a few nips and tucks:

- We start the bullet by summarizing, “A terminal server permitted unauthenticated access”
- We add the consequence and note the security camera exposure. “to sensitive functions including video security monitors.”

The effect of these changes, again, is to lend more immediacy to the finding.

### Long bullets
The “Long bullet” style gives us room to explore a key finding in more detail. The trick with “long bullets” is to state the introductory phrase succinctly. Capture the problem, for example, “Poor vulnerability scan coverage” (in bold). Back it up with facts: “Prolix regularly scans less than half (46%) of its self-identified IP address space for vulnerabilities.” Then state the consequence: “&hellip;which would allow a threat actor to have direct access to Prolix’s internal network—all by guessing a password.”

Here’s an example of a “long bullet” style. with boldfaced key phrases. It begins with a bang—an introductory paragraph that gets right to the point. Two supporting long bullets follow, which follow the _[bold statement] — [fact] — [fact] — [consequence]_ pattern:

> The conditions which facilitated the GS1 ransomware attack exist throughout Prolix’s known internet-facing technology assets. Prolix’s internet-facing assets contain over 100 critical- and high-risk vulnerabilities. Many systems are configured in unsafe ways in contravention to sound and well-established industry practices. Because of the number and kind of these exposures, the level of effort required by an attacker to breach Prolix would be very low. Notable findings include:
> - __Many unpatched critical vulnerabilities__. A cursory scan of Prolix’s reported IP address space identifies over 600 vulnerabilities for which patches are available, many of which are exploited by off-the-shelf attack tools. Over 100 of these vulnerabilities are rated as “critical” or “high” risk, without taking into account Prolix-specific circumstances which will likely drive the true number even higher as they are investigated and closed.
> - __Poor vulnerability scan coverage__. Prolix regularly scans less than half (46%) of its self-identified IP address space for vulnerabilities with its Qualys scanning tools, and it scans only half of its servers.&dagger; Prolix also has an incomplete asset inventory. As a result, Prolix does has no way to know exactly how many vulnerabilies it actually has on its network, and cannot reliably identify which assets need to be fixed.
>
> &hellip;
> 
> <small>&dagger;&nbsp;Prolix identified 143 netblocks as internet-facing, which allows 6,730 possible IP addresses. Only 3,148 of these are registered with Qualys to be scanned. In terms of actual live hosts, only 51%—1001 hosts— are registered with, and regularly scanned by, Qualys.</small>

This example summarizes what we believe: the client is 0wned and will probably get ransomware’d again. Each supporting bullet makes a firm statement and then substantiates it with facts. “Many unpatched critical vulnerabilities” is the bolded phrase. The follow-up sentence provides the essential detail: “a scan identified 600 vulnerabilities&hellip; over 100 are rated as critical or high.” These are not general statements; they are highly specific and quantitative. They are designed to get the reader’s attention, and to persuade.

One last point. Note that we moved some additional quantitative detail to a footnote (“Prolix identified 143 netblocks as internet-facing&hellip;). We could have put that in the long bullet itself, because it provides some valuable additional detail. However, including it would have bloated the length of the bullet. In the end, it made more sense to move it to the bottom of the page.

## Recommendations
McKinsey is arguably the world’s most prestigious management consulting firm. Their partners have a saying that the measure of their worth is defined by the degree to which clients take their advice. QOMPLX believes this as well. If clients do what we say, we make a material difference in their risk posture. By making practical recommendations, we also enhance our own credibility.

To help clients realize the value from their work with us, we need to arm our executive sponsors with enough information to act. Our recommendations should do three things: be _specific_ enough to help the clients understand what they must do, be _ordered_ so they can prioritize their work, and be _short_ enough so they can be digested quickly.

### Bucketing your recommendations
We help clients prioritize their work by putting our recommendations into buckets that they can examine and work separately. Bucketing serves two purposes. First, cognitively, it “chunks” the work so that similar-effort items can be understood as belonging together. Second, it indicates respect for our executive sponsors, because we took the time to consider their circumstances and risk tolerances.

To create buckets of recommendations, consider the whole range of things you want the client to do, ranging from fixing a vuln to hiring people. Write the list on a piece of paper, using unaided recall to pull out the most important things you can remember. Chances are, this list will be a dozen items or less. Then, consider two questions:

- What is the degree of risk of the issue, based on likelihood of exploit or impact?
- How hard is the issue to fix?

Then, group your recommendations into four buckets:
- _Quick wins_—high risk, and low-to-moderate effort to fix
- _Strategic projects_—high risk, and moderate-to-high effort to fix
- _Discretionary fixes_—low-to-moderate risk, and low-to-moderate effort to fix
- _Bear-risks_—low-to-moderate risk, and high effort to fix

A description of each bucket follows:

- _Quick wins_ identify “gimmes”: things our executive sponsors can immediately take action on, and which take a significant amount of risk off the board. Quick wins should not take more than a few weeks to achieve—a quarter at most. They include tasks such as pushing missing patches on external assets, removing stale administrator accounts, performing pen-tests on a limited number of assets, or taking other actions that do not require significant time or money. Our sponsor should be able to easily commission the work. All quick wins are “must-dos.” Your prose should convey _urgency_.
- _Strategic projects_ identify more complex initiatives that will take quarters or years to plan and execute, either because they require substantial focus or money, or because they are intrinsically complex. Examples include globally uplifting incident response, sourcing and implementing a new Identity & Access Management (IAM) platform, or overhauling log management for the company. All strategic projects are “must-dos.” Your prose should convey _importance_.
- _Discretionary_ fixes identify actions that the client should implement, but are optional. For purposes of completeness, use this bucket to capture issues that the client can choose to implement after quick wins, but may not wish to. Including discretionary fixes is another sign of respect, because it signals that we are realists, and not everything can—or should—be fixed.
- _Bear-risks_ are hard to fix, and don’t take much risk off of the table. Use this bucket to keep yourself honest. Do not include any bear-risks in the _Executive Summary_, because they clutter the narrative.

### Structuring the narrative
Begin the _Recommendations_ section by succinctly setting the stage for the specific actions we want clients to take. Describe the context of the assessment. Summarize the “what it means” headlines. Do these things in not more than two paragraphs, of four or five sentences each.

Then, by bucket, make your individual recommendations. Always write recommendations in “imperative voice” (commands). Convey the importance of the work by connecting actions to benefits. Do this, implement that.[^2] If helpful, follow the pattern _[do something]_ to _[gain benefit]_. Here is an example:

> QOMPLX began its assessment by identifying scenarios in which exposed external servers could be used as launch points for a global ransomware attack. Given the significant number of external exposed services, the recent successful ransomware attack on BU1, and pervasive Windows trust relationships, a significant cyber breach would be hard to avoid, detect, or contain. Ransomware groups are taking a growing interest in professional services firms. Prolix looks like an ideal target, with numerous exposures similar to those exploited in the BU1 breach, by the REvil crimeware groups and by related threat actors. Based on minimal diligence, attackers could reasonably expect to be able to steal information, destroy assets and pivot to other assets of interest. The <u>appearance</u> of unpreparedness, in itself, dramatically increases the likelihood that Prolix will be targeted again, and on a larger scale than with BU1.
>
> QOMPLX recommends that Prolix take the following actions to improve the architecture and reduce the risk of a widespread ransomware attack or other serious cyber breach. Our recommendations include _quick wins_ that can be readily implemented, and _strategic projects_ that will require planning and careful implementation. We have not yet included any _discretionary fixes_ that Prolix should consider implementing—all of our recommendations are essential. Optional but recommended improvements will be addressed in later phases of engagement—that is, during program uplift—and linked to Prolix’s risk goals and tolerances.
>
> _Quick wins_ reduce risk with modest effort. Prolix should:
> - __Immediately complete containment and uplift activities at Business Unit 1__ to deeply understand the incident and bring the network up-to-par, aligned with Prolix’s US security program
> - __Accelerate already-purchased deployments of QOMPLX Privilege Assurance__ globally, to gain visibility into all global Windows trust relationships that could facilitate lateral movement across Prolix regions—enabling Security and IT leadership to understand potential upcoming decisions (e.g. region isolation) in another event with superior business context
> - __Develop a comprehensive, global asset and risk inventory__. Prolix can build an initial inventory of IT assets and risks with modest effort to protect against additional ransomware attacks and to aid prioritization. This effort can pave the way for a strategic asset and risk register that is ingrained into global security and technology programs, and is integrated with Prolix’s future cloud architecture.
>
> _Strategic projects_ will take more time to plan and execute. Prolix should:
>
> - __Evaluate the security of future Prolix acquisition targets__, and create standard processes to reduce cyber risks associated with merger and acquisition activities
> - __Supplement the global security program__ with services to fix risks identified by Prolix’s CISO and QOMPLX, and achieve ISO 27001 compliance
> - __Review and re-design of the global Active Directory environment__, providing much-needed security and IT program improvements, and setting conditions for Prolix’s broader modernization initiatives.

You can see in the example above that the “quick wins” and “strategic projects” all begin with strong, action-oriented imperative verbs: _complete_, _accelerate_, _review_, _re-design_, _evaluate_. They also connect actions to benefits—the what and the why. For example, the action “Evaluate the security of future Prolix acquisition targets, and create standard processes” connects directly to the reason: “reduce cyber risks associated with merger and acquisition activities.”

Here’s another example of a _Recommendations_ section:

> Retail operational environments process large volumes of customer’s personal and payment card data, both of which are highly valued by attackers. Because of the weaknesses discovered during the initial assessment, QOMPLX recommends that Fresh Retail immediately assess all segments and VLANs in their internal and external networks. We also recommend reviewing the completeness of Fresh Retail’s overall security program to ensure that appropriate controls are in place to reduce Fresh’s overall risk and protect its data.
>
> Our recommendations include quick wins that can easily be implemented, and strategic projects that will require planning and careful implementation. We also describe discretionary fixes that Fresh Retail should consider implementing, at its option.
>
> Quick wins reduce risk with modest effort. Fresh Retail should;
> - Assess the entire organization, internally and externally, to build a list of assets that are unmanaged, or in need of immediate fixes.
> - Apply available security fixes to all devices.
> - Upgrade or replace out-of-support operating systems.
> - Ensure that remote access tools, such as VNC and Remote Desktop, use strong passwords.
> - Disable any services or applications which are not required by operational needs.
> - Create a policy for retaining logs, as required by regulations, statutes and contracts, and implement the policy.
> - Implement monitoring tools for validating authentication traffc and detecting credential forgery in its operational environment.
>
> Strategic projects will take time to plan and execute. Fresh Retail should:
>
> - Audit all software and all hardware inventories to confirm accuracy. Devices that are not visible to the organization can be leveraged by attackers that have already gained internal access and are seeking hosts for lateral movement.
> - Implement continuous vulnerability management. Threat actors take advantage of the time periods between the disclosure of new vulnerabilities to the implementation of fixes by customers. Fresh can shrink its window of vulnerability by implementing a continuous
vulnerability management program.
> - Configure assets to common baselines. Deploy approved security configurations for all hardware, network devices, software, laptops, workstations,and servers to ensure that configuration settings with durable security properties are deployed.
> - Ensure that all critical security systems and devices send logs to the security event management system Fresh uses; minimally, these should include VPN servers, intrusion detection systems, and authentication-related services such as single-sign-on systems, federated identity providers, and its most important third-party SaaS providers.
>
> As a reference, Fresh should consider using the Center for Internet Security’s CIS Controls (see the section that follows).

### Actions Already Taken
Few clients appreciate being told their environments are messy, or at risk of a significant cyber-attack. To help build consensus to implement our recommendations, consider including an _Actions Already Taken_ section. This allows executive sponsors to give credit for good work their teams have already done. Write this section with a boilerplate introduction, and follow with a short number of long bullets. For example:

> QOMPLX staff have been actively engaged with Prolix’s team members to address issues identified during the engagement. Prolix staff has taken the following actions since the original issues were identified:
> - __Reviewed backup procedures for all Active Directory domain controller assets__, ensuring backups of key Windows configurations, client matters, and offline systems that are not connected to Prolix networks.
> - __Notified asset owners about key vulnerabilities__. QOMPLX worked with Prolix to notify identified system owners about high- and critical-risk vulnerabilities affecting their assets. As of this writing, the Prolix team has fixed about half of these, and committed to fix the remainder by the end of August.
> - __Initiated a vulnerability tracking process__. Because no robust internal processes for vulnerability tracking exist, QOMPLX is collaborating with Prolix to build an independent vulnerability tracker.

# Wrapping up

So there you have it.

Done right, strong Executive Summaries distill complex information into advice that clients can understand and apply. By beginning with a discusson of the context of your work (“background”), you build credibility. By separating facts (“findings”) from advice (“recommendations”), you create incentives for clients to focus on their responses to the issues you raise, rather to debate the facts. And by bucketing your recommendations based on risk and effort, you give the clients choices about much time and money they can choose to spend. Not all clients will agree with all of your conclusions. But even when a client doesn’t heed your advice, you can rest assured that the urgency and importance you meant to convey will come through.

_In the next post in this series, I discuss how to write a high-impact Red Flags document—a short, dense, bottom-line summary of what an corporate buyer needs to know about the cybersecurity posture of a target company._

[^1]: The last sentence is a “zinger” that succincntly combines an opinion with facts explaining why we hold that opinion.

[^2]: I wrote this entire paragraph, and indeed, most of this post, in imperative voice.