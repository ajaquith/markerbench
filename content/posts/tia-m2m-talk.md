---
title: "Cybersecurity for Machine-to-Machine (M2M) Networks"
summary: Billions of internet-connected devices are now online and talking amongst themselves. To secure them, vendors need to design them to avoid surprises they didn’t intend.
authors:
 - arj
date: 2013-06-04 16:00:00 +0000
tags:
  - cybersecurity
  - risk
aliases:
  - /blog/2013/06/04/tia-m2m-talk/
---
_This is the nominal text of panel remarks I delivered at the Telecommunications Industry Association's M2M & Cybersecurity Workshop on June 4th, 2013. The objective of the panel was to discuss the following topic:_

> Define a cohesive vision for a secure, reliable and economically viable machine network. What are the key objectives and what level of risk can be tolerated?

Good afternoon. I am Andrew Jaquith, the CTO of SilverSky, a leading cloud security provider. It's great to talk to you today. You may not know SilverSky, so first, a little about us and our qualifications:

<!-- more -->

* SilverSky protects our customers' most important information. We manage customers' email and collaboration, secure their data with our security software, and monitor their infrastructure for compromises, all from our cloud.
* We have 6000 customers, mostly in the private sector, including 1800 in the most risk averse and security sensitive industry there is: financial services
We filter 50 million emails a day, and analyze 425 million security events
* We protect half a trillion in banking and financial assets
* We have a growing presence in telecommunications and communications service providers. We partner with Cbeyond, Telepacific, NTT, Windstream and — thanks to an an acquisition we are announcing tomorrow — with XO and Peak10

While we aren't a device maker or carrier ourselves, we see a large volume of network traffic and security events every day. We see a lot of activity and have an perspective of what's going on in the private sector.

Let's talk about machine-to-machine (M2M). M2M means any digital, network-protected device that is part of a larger system. The "M" in M2M means something with an IP address. Everything from ATM machines to smartphones to copiers to energy grid sensors to that networked refrigerator we've all been predicting — at least, ever since MIT networked its soda machine in the early 1990s. I remember as a young pup around 1993 when Novell predicted that one day, there would be 1 billion network-connected devices. That prediction seemed audacious then; it is merely quaint now.

The "2M" part of M2M means that connected thing is a node in a larger network, and that the communications are only partially directed by a human. A consumer, for example, might own a mobile phone. They will surf the web, buy their kids gifts on Amazon, and play Words with Friends with, well, their friends. There's nothing about these activities that is different or more interesting than what we have seen on the PC. However, all of the supporting services underpinning the mobile experience — cellular data communications, background telemetry, push notifications, carrier updates — that is all M2M traffic. So are the networked soda machine replenishment signals, SCADA traffic, the cellular tower updates, etc. These are not initiated by humans; these are all machines talking to machines.

The reason we are all here: talking about security in M2M. We are here, I think, because so much of what we experience and take for granted every day relies on networking; that is, the "2M" part. Increasingly, all of that networking is under the covers, and not directly perceived or controlled by the consumer or end customer. It is of paramount importance, therefore, that we can trust the networks, devices, clouds and data that underpin the M2M economy. We need to trust the things that filter the water we drink, transmit the power we consume, and connect us to other people.

What is does success at securing M2M look like? With something as diverse as M2M, one cannot easily articulate a "vision" for security. There is no single "system" one can articulate a vision for. It's a "system" in the same way that health care is a system: fragmented, partly analog, few standards, and filled with many parties with competing interests.

But the need is clear. Risks abound across the system. A popular grey-hat security research project, for example, has released automated exploits for SCADA systems from Rockwell, GE, Schneider, Siemens and many others — making it relatively easy for attackers to weaponize and use on a large scale. Scary. And these are people who are supposed to be our friends. Then there are those who are not our friends: nation-states such as China, Russia and Iran, which have funded large offensive cyber-warfare teams. It is certain that M2M systems are on the target list.  Rounding out the list of threat actors includes the usual criminal gangs, unsavory hackers, miscreants, attention-seekers, pirates and — arguably the worst of the bunch — Mr Murphy (as in Murphy's Law).

So, defining a vision for M2M is arguably a fool's errand. That said, if I could suggest one big hairy audacious goal for M2M security, it would be this:

> The absence of surprise

"Surprise" in the context of M2M means disrupted business, theft of service, successful attacks on critical infrastructure, civil unrest, loss of life or livelihood, theft of secrets or corrupted data. Drilling down a bit more, "absence of surprise" implies four other goals. It implies:

* _Designing for failure_: having compensating processes for dealing with compromises
* _Designing for resilience_: making it possible to diagnose, upgrade in the field, and have robust functions in less-than-optimal environments
* _Eternal vigilance_: having a strategy for continuous monitoring; for incident handling, and for response activities (often neglected)
* _Risk management_: eyes-open knowledge of what adverse events are acceptable, and how frequently they can be tolerated

Let me illustrate by example. Ten years ago I helped design of a security subsystem for some hardware devices due to be deployed by one of the most zealous and security conscious organizations around. This organization would do just about anything to ensures that their mission was achieved, that their devices were not compromised, and that they were as protected as possible from the threat posed by attackers. No, I'm not talking about the military, the CIA, or the NSA. I'm talking about cable TV.

The job was to design Comcast's next-generation conditional access system (called DCAS aka True Thru-Way). What was the goal? To design a bulletproof CAS that would securely deliver any programming of the customer's choice, so they could get anything they wanted _and_ paid for. _But_ — and this is important — not what they didn't pay for. Also: nobody else could get the programming without paying either. The system we designed had a three key features designed to advance this goal:

* _Device integrity_: keep the device in a known state. This implied that we needed not just a way of keeping a set-top box (STB) from being tampered with, but a way of knowing when it was being tampered with.
* _Content protection_: require encryption between the cable network head end and the STBs. A strategy for hardening the box. Creating a cryptographic "key ladder" with long-lived session keys and ephemeral ones, so that compromising a more frequently used key meant a finite window of time for the compromise. We also needed "secure elements" on the box that would be "personalized" for each unit.
* _Device updates_: develop a way of revving the local STB firmware and updates. That implied having a "root of trust" derived from keys that were managed centrally. We know from watching the experiences of DirecTV (and today, Apple) with "hackers" that adversarial warfare with determined opponents makes defenders stronger.

What this meant in our case: lots of crypto. Serious review and iteration. Willingness to learn through evolution. Knowing that you have to walk a fine line between between security robustness, flexibility, usability and ability to manage at scale in the field. Perhaps most important: all of the design decisions were informed by an acceptance by Comcast of exactly how hard it ought to be for a pirate to pop a box and get free TV. How hard should it really be, and what would the company tolerate? Also, Comcast defined which "tail risks" they wanted to avoid. That is, what does catastrophic failure look like? In this case, just for example, Comcast wanted to make sure that other than stealing the topmost root key — which was made very, very difficult — no mass compromise was possible; an attacker would have to go box-by-box.

This should give you an idea of what is required to build devices with high levels of security, where that security supports the business goal. For a more modern example, look at Apple's iPhone. That is a great example of fairly robust security and usability. Fifteen years ago, if I told you that you would see the rise of a consumer computing platform with over 500 million units deployed, where the entire platform includes trusted boot, mandatory access control, full device encryption, mandatory application screening, mandatory application signing from a central authority, a vibrant developer scene, and very little (essentially zero) malware, and one that doesn't drive customers batty — indeed is one heck of a pleasure to use — you'd say I was nuts. But yet that's what we have. I don't advocate Apple's model _per se_. But it illustrates one way to try to accomplish many goals, and do them all well enough that the net risk to consumers is very low.

On the other side, look at what happened with Stuxnet. The attack was essentially via USB stick plus a stealthy worm that attacked Siemens SCADA systems used to control and monitor centrifuges for enriching uranium. This system runs a variant of Windows. Very few of the ideal security characteristics one would like to see in a robust, secure embedded operations system were in place in this case. (Arguably in the case of Stuxnet this was a feature rather than a bug.)

My wish for the industries that are involved in M2M, looping back to my original comment, is that we design collectively and individually for the absence of surprise. Any surprises you get should be those you expect... And then, of course, they aren't surprises. They fall into the category of what Donald Rumsfeld memorably called "known unknowns." Our eyes are wide open, based on enlightened economic self interest. In addition, I would hope that have enough eyes wide open that many of the "unknown unknowns" are imagined as well.

That won't be good enough in all cases, though. In closing, we will need to consider incentives to swing the calculus to align economic self interest with good security outcomes. Speaking as a trained economist who works in the security field (and who programs to relax), almost all security failures are rooted in perverse economic incentives. Our goal ought to be to align incentives so we get better outcomes. In my view, everything should be on the table: software security liability for manufacturers, legal shielding for sharing of security data and incidents, promotion of industry standards and inclusion of these standards in purchasing guidelines, and, in cases where the risks demand it, regulation or legislation.

If we do all of these things, we will have successfully used our collective imaginations to identify, reduce, or willingly accept the M2M risks we face, both today and in the future.

Thanks very much for listening.