---
title: "Microsoft to CIOs: Drop Dead"
description: Microsoft’s new advice for securing Active Directory does customers a disservice by focusing on the wrong things. Tomorrow’s “Zero Trust” and Azure roadmaps won’t stop today’s ransomware epidemic. Enterprises need to protect the Active Directory they’ve already got.
author: arj
date: 2020-12-22 12:00:00 -0400
image: /images/drop-dead.png
featured: true
comments: true
tags:
  - security
  - vendor-bashing
  - microsoft
---
_Note: This article originally appeared on the QOMPLX, Inc blog._

A few days ago Microsoft released updated guidance as part of its [“Privileged Access Strategy”](https://docs.microsoft.com/en-us/security/compass/overview?ref=qomplx.com) series for customers. Ostensibly about methods for securing privileged access to Windows network resources, buried within it was something surprising:

> The Enhanced Security Admin Environment (ESAE) architecture (often referred to as red forest, admin forest, or hardened forest) is a legacy on-premises approach to providing a secure workstation for Active Directory administrators that has been retired from mainstream Microsoft recommendations. (_Source_: [ESAE Retirement](https://docs.microsoft.com/en-us/security/compass/esae-retirement))

Red Forest was Microsoft’s recommended architecture for securing Active Directory. It describes a strategy for making AD more resilient to large-scale attacks, such as those from ransomware actors. In its new guidance, Microsoft has declared Red Forest dead—even as it continues to implement something similar internally. It replaces prior guidance to use the Red Forest architecture with a series of “best practices” that include using of multi-factor authentication, using Privileged Access Workstations (PAWs) to constrain access paths, putting “Zero Trust” everywhere, and adding a heavy dose of Azure Active Directory. On-premise is declared to be an anti-pattern, replaced by many more belts, a closetful of suspenders, and an embrace of the Microsoft cloud, which requires the costly E5 enterprise license.

# When Zero Trust Isn’t

Many of these concepts contradict each other. For example, there is Microsoft’s emphasis on [“Zero Trust” networking](https://go.forrester.com/blogs/category/zero-trust-security-framework-ztx). My good friend John Kindervag coined that term while we were both analysts at Forrester—thereby ensuring he could die a happy man with “Zero Trust” chiseled on his headstone. It describes a strategy for staying secure despite not being able to trust endpoints or networks. The result of which is you spend extra effort authenticating the operator, and the devices they use. But what Microsoft calls “Privilege Access Workstations” are really heavily-armored  PCs that are highly trusted for administrative functions. And being a domain-joined Windows Workstation (“binding to Active Directory”) means you are trusted in a way that an ordinary Macbook Air on the network, for example, is not. In short: Windows networks are _highly trusted_ networks, not Zero Trust.

Moreover, Microsoft’s advice to deprecate on-premises Active Directory and move things to Azure comes just one week after it admitted that, like many of its customers, it was a victim of the [SolarWinds attack](https://www.theverge.com/2020/12/17/22188060/microsoft-president-solarwinds-orion-hack-breach-brad-smith), part of a state-sponsored cyber campaign. Microsoft’s Brad Smith did not say whether Azure was compromised, saying only that its “environment” contained the tainted SolarWins binaries, and indicating that as yet they had “found absolutely no indications that our systems were used to attack others”—hardly definitive and not comforting to CIOs.

Let’s back up to understand why Red Forest exists at all. There is no doubt that in developing the concept in 2016, Microsoft understood the _symptoms_ of today’s Active Directory issues excruciatingly well. In a 2017 RSA Conference presentation called [“Critical Hygiene for Preventing Major Breaches”](https://published-prd.lanyonevents.com/published/rsaus17/sessionsFiles/3774/CXO-F02-Critical-Hygiene-for-Preventing-Major-Breaches.pdf) two Microsoft presenters, plus another co-presenter from the Center for Internet Security, accurately described what attackers do in a critical breach: they go after privileged access. That includes:

1. Getting a beachhead via a phishing attacker or other technique
2. Moving laterally to other hosts by stealing credentials
3. Escalating privileges to become domain admin
4. Executing the attacker’s mission, including stealing data, destroying systems, and taking up residence in the network

Accurate so far. As we’ve said elsewhere, succinctly: [get in, spread, profit](https://www.scmagazine.com/news/-/attacks-on-authentication-turn-ransomware-from-disruption-to-disaster)! Fast-forward four years, and the playbook remains the same. It is clear that Microsoft accurately described the symptoms. It is not clear that the company understands the disease, which is, quite simply, that Active Directory puts too much power in the hands of a few people. Consider the range of services Active Directory provides; it is:

- A _list of users and their relevant contact details_ such as account IDs, full names, email addresses and phone numbers
- A _list of servers and workstations_ known to the administrators (“bound to the domain”)
- An _authentication service_, which allows employees and contractors to log in so that they can use privileges granted to them to do their work
- A _security policy enforcement service_, which pushes down password, screen-lock and network restrictions (“group policies”) down to workstations and servers
- A _lightweight entitlements repository_, by virtue of its use of built-in and custom groups, which have entitlements for various privileged activities. Åctive Directory, for example, has over fifty (50) [built-in privileged groups](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/appendix-b--privileged-accounts-and-groups-in-active-directory), ranging from Enterprise Admins and Account Operator, to “DnsUpdateProxy” users
- A _lightweight configuration management database_, which allows printers, servers and other devices to be configured and deployed
- A _security boundary_, as enforced by forest trusts

# Privilege Concentration Root of AD Security Issues

Microsoft’s guidance is intended to help enterprises make privileged access more difficult to abuse, and to make it used much less often. Those are nice goals. But focusing on privileged access isn’t the point. It’s privilege concentration that matters. Getting Domain Admin privileges is supremely valuable to attackers, because after you get domain privileges, you can use your newfound powers to burn every Windows user or computer to the ground. Even with Red Forest, which is designed to split administrative privileges into multiple forests, Domain Administrator privileges in the less trusted “computers forest” can _still_ burn every Windows computer to the ground.

Active Directory is an overstuffed turkey, offering a range of services from authentication to configuration management to policy enforcement. No matter what new practices Microsoft prescribes, it’s still overstuffed. [That’s why we have a ransomware epidemic](https://www.qomplx.com/news-analysis-privilege-escalation-features-pop-up-malware-variants/). It is precisely because AD has its hooks into workstations, servers, and user accounts that ransomware works. Nothing in Microsoft’s new guidance changes that. No efforts to make administrative privileges harder to use will make those privileges less concentrated.

_Active Directory is insecure. Throwing it out isn’t the answer; protecting it is._

Active Directory does so much, and is so complex, that it cannot be effectively secured. The company’s low-key announcement this month is just official recognition that Microsoft has thrown in the towel. While not surprising, it is unwelcome news for tens of thousands of enterprises. If you have an on-premise Active Directory implementation, you’re dead to Microsoft unless you move to Azure. To paraphrase the New York Daily News’ [infamous headline about President Ford and New York City](https://www.criterion.com/current/posts/4707-the-daily-ford-to-city-drop-dead-new-york-in-the-70s): “MSFT to CIOs: Drop Dead.”

{{< figure src="/images/drop-dead.png" height="400px" title="Image: Parody derived from Wikipedia image, copied from http://pqasb.pqarchiver.com/nydailynews/pageprint.html. Intellectual property owned by New York Daily News." >}}

Enterprises don’t need a complex new belt-and-suspenders architecture or Microsoft’s magic cloud to secure something that fundamentally cannot be secured. What enterprises need, instead, are practical solutions that help them detect and stop attacks now. These include tools to [validate the Kerberos authentication protocol](https://www.qomplx.com/cyber/identity/) that lies at the heart of Windows networking, powerful diagnostics that [help security teams understand attack paths](https://www.qomplx.com/cyber/privilege/), and analytics that predict their company’s potential susceptibility to abuses of privilege.

Enterprises live in reality. And in that reality, they have substantial investments in Windows infrastructure. That infrastructure is being ransacked by criminal ransomware gangs and state-sponsored actors—such as those behind the breach of SolarWinds and 18,000 of its customers. The answer to recent supply chain attacks can’t be, place your trust in Microsoft, because as a trusted supplier, Microsoft can reduce your supply chain risks. That’s circular logic. As we’ve noted already, Microsoft’s recent track record protecting its own infrastructure is far from spotless.

Privilege escalation and credential forgery attack vectors can’t be roadmapped or (white)papered over. These tactics are behind [every major security breach of the last five years](https://www.qomplx.com/manykatz-how-active-directory-hacks-went-mainstream/). And as earnestly as Microsoft may tell its customers that Azure is the answer, ransomware operators won’t stop attacking just because Azure AD might someday be useful. Multinationals won’t stop suffering losses in hundred-million-dollar increments because Microsoft discovered “Zero Trust Networking”—with no way to genuinely implement it as long as domain-binding makes some things More Trusted Than Others. And Russia won’t halt its campaign to steal our nation’s most sensitive industrial, medical and military secrets while waiting for armies of MCSEs to complete their Azure migration projects.

Active Directory is here to stay. It remains central to the end-user computing plant of most organizations. And although application teams have moved a substantial fraction of new application development to platform-independent stacks, many enterprises continue to run vital and business-critical application workloads on Windows. Protecting it is job one.

Let’s get to work.