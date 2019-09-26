---
title: Why CISOs should Care About Cloud “Drift”
author: arj
created_at: 2019-09-25 12:00:00 -0500
layout: post
categories: 
- security
- DevOps
- applications
- metrics
image: aws.jpg
comments: true
---

# Why CISOs should Care About Cloud “Drift”

_Author&rsquo;s note: this is the first in a series of posts on cloud security._

A funny thing happened in many of the world's most rarefied boardrooms. Over the last five years, CEOs realized they [aren&rsquo;t in the datacenter business any more](https://www.jpmorganchase.com/corporate/investor-relations/document/ceo-letter-to-shareholders-2018.pdf). CIOs and Chief Digital Officers now have a new mandate: move their companies&rsquo; applications and infrastructure into public cloud services as fast as possible. The prospect exhilarates technologists, but scares security teams. Nobody wants to be the [next Capital One](https://krebsonsecurity.com/tag/capital-one-breach/), even though most companies would kill to have had the [nine years of digital transformation experience under their belts](https://aws.amazon.com/solutions/case-studies/capital-one-devops/) that Capital One had at the time of its breach.

Solutions to the cloud security problem cannot be tackled in a single post, other than in a very generic way. That would be rather unhelpful. For this reason, instead of zooming out, I'd like to zoom _in_ and talk about a critical point of leverage that every Chief Information Security Officer (CISO) should focus on: managing the _drift_ related to their cloud-based applications and infrastructure. As I will explain, the wholesale movement of large workloads to cloud service vendors such as Amazon Web Services (AWS) brings with it new tools and processes. These tools and processes can be profitably exploited by savvy CISOs. By keeping a careful eye on the _rate of drift_ of their technology assets, CISOs can provide evidence to their boards and auditors that their cloud deployments are well-managed. Well-managed cloud deployments are, by definition, less risky because they are easier to change in a controlled way, and more stable as well.

## What is Drift?

What do we mean by &ldquo;drift&rdquo;? The Oxford English Dictionary defines _drift_ as &ldquo;a steady movement or development from one thing towards another that is perceived as unwelcome.&rdquo; In finance, [stochastic drift](https://en.wikipedia.org/wiki/Stochastic_drift) refers to the change in the average value of a random process. That works well for stock prices and interest rates, which [seem random to the average investor](https://www.amazon.com/Random-Walk-Down-Wall-Street-ebook/dp/B00QH9NTSI).

In technology, the processes that build cloud-based applications and infrastructure &mdash; including those associated with agile development, continuous integration and continuous delivery &mdash; are _not_ random. They are stateful and should (fingers crossed!) work the same way every time. So in cloud deployments, drift is more straightforward to understand: it is simply the divergence from an expected state. By &ldquo;expected state&rdquo;, we mean the intended configuration of an application and its supporting infrastructure, as encoded in configuration management scripts and tools. 

Before the widespread adoption of cloud computing, the primary methods for documenting and deploying applications and infrastructure included an odd assortment of Visio diagrams, wiki pages, SharePoint sites, Word documents, READMEs and runbooks. In the cloud era, datacenters and all of their workloads are entirely software-defined. You can now declare your intended state _in code_. A variety of tools then provision, configure and deploy all of the resources needed to make that state a reality. The tools are absolutely integral to the process because they enable technology teams to scale, ensure consistent processes and eliminate manual errors. You can stand up an entire cloud-based compute environment from a single command in less than five minutes.

Here&rsquo;s the important point. _Because configuration tools are at the heart of all modern cloud-based delivery proceses, they can be profitably exploited as a data source to understand drift._ Here's how to do it.

## _Drift_ as a Metric

For instance, suppose you have an application that is provisioned by a cloud configuration management tool, such as [Terraform](https://www.terraform.io), [AWS CloudFormation](https://aws.amazon.com/cloudformation/), [Ansible](https://docs.ansible.com/ansible/latest/index.html), [Chef](https://www.chef.io), [Puppet](https://puppet.com), [CFEngine](https://cfengine.com), and [SaltStack](https://www.saltstack.com). These tools provision, configure and maintain the state of applications and their accompanying infrastructure. They are also sources of data you can mine to your advantage.

Here's a real example. My [securitymetrics.org test application](https://github.com/ajaquith/securitymetrics-aws) runs in AWS and is configured using a Terraform plan and an Ansible playbook. The Terraform plan creates 38 AWS resources, including two servers (&ldquo;EC2 instances&rdquo;), a private virtual cloud, network routes, host firewalls (&ldquo;security groups&rdquo; in AWS-speak), identity policies, randomized passwords, Docker containers, and other resources. The Ansible playbook configures the two hosts created by Terraform, running 121 tasks to bring them into an expected secure state. In sum, these plans and playbooks make, test and fix (if necessary) 159 [&ldquo;promises&rdquo;](https://www.oreilly.com/library/view/thinking-in-promises/9781491917862/ch01.html) about the state of the application and its accompanying infrastructure.

Drift is straightforward to calculate: execute the plan, and run the playbook. Then, count the number of changes. This is the _amount of drift_. Divide by the number of tasks. The result, expressed as a percentage, is the _drift rate_.

More formally, the _drift rate_ is:

$$\frac{# changes}{# changes - # skipped tasks}$$

               # changes
      ---------------------------
       # tasks - # skipped tasks 

Note that we remove &ldquo;skipped&rdquo; tasks from the denominator so that the results are not polluted by tasks that did not need to run for some reason or because they did not apply.

Here is a worked example:

- The Terraform plan verifies correct state for 38 AWS resources, and indicates that 1 change is needed. The drift from the expected configuration is 1, and the drift rate is 2.6% (1 out of 38 resources).

- The Ansible playbook runs 121 tasks, skipping 50 because they do not apply to these particular EC2 instances, and completes with 4 changes. The drift from the expected configuration is 4, and the drift rate is 5.6% (4 out of 71 tasks).

The total drift rate for the full stack is therefore 4.6% (5 out of 109 task and resource promises). Because I am working on the environment, that amount of drift is expected. In a steady-state situation, however, I would expect the drift to be zero.

Drift metrics are easy to create. In the case of Ansible and Terraform, the source data comes straight from tool output. Only a few lines of shell script are needed to dig out the data we need. And it is easy to wire up a batch job (for example, an AWS Lambda task) to re-run these tasks on a regular schedule, for example daily, so that the environment measures verifies its configuration (and self-heals!) once a day.

# Using Measurement of Drift Strategically

The drift rate gives CIOs and CISOs a view into how consistently their technology assets conform to a desired state; in essence, how well the promises they have made about their configurations are being kept. Applications and infrastructure with higher rates of drift are less well-managed than those with lower rates.

Managers can use drift metrics strategically to identify opportunities to improve performance. Any of the standard analytical strategies are appropriate. For example, you can:

- Group all assets by their owning business units, and compare business units&rsquo; drift rates to identify the best and worst performers

- Track drift rates over time to identify which parts of the organization have less-consistently-well-managed technology assets than others

- Keep separate drift metrics for each class of asset, for example, networks/infrastructure versus host/applications

- Divide assets into &ldquo;in development&rdquo; and &ldquo;steady state&rdquo; populations, and create a tools adoption target for the former population, and a drift rate target for the latter

You need not go overboard. Pick one or two strategies to start with. The old chestnut about &ldquo;what gets measured, gets managed&rdquo; applies here.

# What Drift Does Not Address

Now that you understand how to calculate the drift in your cloud environments, it is worth mentioning its limits. Drift is a crude metric, capturing only the aggregate number of changes to a technology stack. In addition, it is silent about whether particular state changes are actually important. For example, if Terraform detects that a firewall rule was somehow changed to &ldquo;any-any&rdquo; from its expected single-host/single-port configuration, that might be a big problem.

And lastly, drift _per se_ does not help CISOs understand whether the desired state is actually any good &mdash; or complete. Yes, the CIO can move the organization to an &ldquo;infrastructure as code&rdquo; mindset, and then marshal the tools, people and processes to make it reality. Yes, this is awesome for agility and necessary for transformation. But these things in and of themselves do not ensure that the CISO's _control objectives_ are reflected in the configuration code. That takes work. I will discuss this topic in a future post.

Nonetheless, measuring the drift rates for your cloud-based applications and infrastructure is an effective proxy for understanding how well-managed they are. The drift rate is a concise and simple metric that you can cut, mash up and measure many different ways to understand where your trouble spots are.

Thanks for reading!

_Image credit: [AWS - Amazon Web Services Office in Houston, Texas](https://www.flickr.com/photos/87296837@N00/46600198075) by [Tony Webster](https://www.flickr.com/photos/87296837@N00) is licensed under [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/?ref=ccsearch&atype=html)._
