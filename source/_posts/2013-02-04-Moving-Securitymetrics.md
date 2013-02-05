---
title: "Moving securitymetrics.org to Octopress"
created_at: 2013-02-04 00:00:00 +0000
layout: post
categories: 
- security
- web websites
- applications
comments: true
---
Soon, I will be moving the securitymetrics.org website to a simpler, secure and more usable system -- the same platform that powers Markerbench. It should be done in time for Mini-Metricon (March 1st, 2013).

Some background. When I started [securitymetrics.org](http://www.securitymetrics.org) in 2004 with Dan Geer and Kevin Soo Hoo, I had visions of making a cool, collaborative website for it. I liked the "wiki" philosophy (simple markup, text-based) and thought it would work well as a lightweight collaboration platform. I was, at the time, the co-author/co-architect of [JSPWiki](http://incubator.apache.org/jspwiki/), an open source JEE-based wiki package. Because it contained a lot of my code, went the reasoning, I'd know just whose throat to choke when things went wrong. I could customize the server in all sorts of ways when I wanted to. And as a side benefit, I'd get to demonstrate my mad enterprise skillz by using JSPWiki's four-tier architecture (client, web server, app server, database). That was the theory.

But a few things happened between 2004 and now:

* Competing content-management systems -- like Wordpress and Drupal -- got better and better. With bigger dev teams came more features. The wiki software hasn't kept pace -- no social integration, for example.
* Spammers overran my wiki self-registation system. As a result, I was forced to disable additional registrations, rendering securitymetrics.org not very collaborative at all.
* I discovered I hated maintaining and upgrading that four-tier architecture I had been so proud of.
* The wiki server's memory leaks meant it needed monthly reboots -- if I remembered. If I didn't, it meant lots of downtime.
* The threat environment got a lot nastier, leaving me leery of running ANY kind of content management server, never mind a wiki server.
* I got married. No explanation needed here, I suspect.

It has been clear for a while that securitymetrics.org needed something better. Something simpler, more secure and (preferably) social. After a long period of on-and-off searching, I found something pretty close to ideal: [Octopress](http://octopress.org).

As I've written before, Octopress is a [static website generator](/blog/2013/01/08/static-blogging/); it is derived from Jekyll. You can think of it as a website "compiler." You feed it text files, and it emits lovely HTML, CSS and JavaScript with all of the modern goodies built-in: discussion threads and comments via Discus, social integration via Twitter, Google and Facebook "like" buttons, search via Google Simple Site Search, and site traffic analysis via Google Analytics. The best part is that all of the components are 100% static. There are no application servers, no databases, no users; and, no user input accepted or stored. All of the dynamic behaviors result from loading up various bits of client-side JavaScript to invoke other people's stuff. That makes the attack surface pretty close to zero. And, because everything is static, all that static stuff can be WAN-accelerated until it screams, and stored just about anywhere (Amazon S3, GitHub Pages, Heroku) without worry.

What does this mean for securitymetrics.org?

* We will switch over to the new site at or around Mini-Metricon on March 1st.
* The new website will be better looking and much better organized. I've edited and re-organized ALL of the Metricon content, for example, while I was at it.
* I will be the sole "publisher" of the website, at least for the time being, but welcome all collaborators.
* We will have a new workflow for people who want to write on the securitymetrics blog. It will involve Markdown and DropBox.
* After Mini-Metricon I will probably move the mailing list to a new, faster, provider (first things first: website, then listserv)

For those of you who will be attending Mini-Metricon, I am looking forward to showing you the new site.