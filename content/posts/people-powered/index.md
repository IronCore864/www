---
title: "People Powered - Solid Action Items to Build Your Open-Source Community from Scratch"
author: "Tiexin Guo | 郭铁心"
authorLink: https://www.guotiexin.com
tags: ["open-source", "community"]
categories: ["Open-Source", "Community"]
date: 2022-06-13

cover:
  image: "panda.jpg"
  alt: "panda"
---

## 0 "People Powered" -- the Book

Recently I read a book recommended by my boss: [People Powered](https://www.amazon.com/People-Powered-Communities-Supercharge-Business/dp/1400214882).

A a good book, by any means.

- It explains what a community is and why you might need it.
- It categorizes communities into three different types and you can see to which type your project belongs.
- It teaches you how to write the value statements of your community. - It created a SCARF model to recognize your audience.
- ... and a lot of other valuable things.

However, I don't like this book. When I say "I don't like this book," I mean "I don't like this book, at all." If you haven't read it, don't. Save yourself $9.78 and 3 hours of your life.

Well, I'm not saying that I don't like this book because it's wrong. This book isn't wrong. It's the opposite of wrong because it's all true.

I'll give you an example. There is a chapter "SIX FOUNDATIONAL KEY PRINCIPLES AND HOW TO APPLY THEM":

> 1. Start Simple and Build Valuable Assets
> 
> 2. Have Clear and Objective Leadership
> 
> 3. Clear Culture and Expectations
> 
> 4. Focus on Relationships, Trust, and Engagement
> 
> 5. Strive for and Be Reactive to Insight
> 
> 6. Be Surprising

I'm extremely pissed, by this section.

Yes, they are all true, but they are utterly meaningless: what, are you suggesting that I should start with complexity and build invaluable assets first? Are you saying that I shouldn't have clear leadership? Are you suggesting we embrace an obscure culture? Focus on Relationships, Trust, and Engagement? Is this marriage counseling or community building? And be surprising? What does that even mean?

These are all true, but they have little value (if any) in guiding your actions. 

This is precisely why I don't like it: it says all the true stuff, most of which you might have already been familiar with, but it doesn't tell you a single action to achieve those true statements.

It's like saying "if you want to lose weight, you need to eat healthily and eat less" without defining "healthy" and calculating base metabolic rates and food calories.

It's like saying "I'm teaching you how to fly a plane. Step 1: get into the plane. Step 2: strap on the safety belts. Step 3: fly it."

It's true, but it's not extremely helpful.

And that is why I decided to dive deep into this "community building" matter and give it a try myself.

Without further adieu, let's get started.

---

## 1 Motivation

First, let's talk motivation.

- Why should I join an open-source community?
- To be specific, why should I join _YOUR_ community?
- Why should I contribute?
- Why don't I simply use the product and never contribute back to the community?

After all, it's free and open-source. I _DO NOT have an obligation to contribute_, right? 

This might sound cynical, but my best is that many people think like that, for real. Most people are the "silent majority" in the open-source world where they are simply users, not contributors. Me included. Guilty as charged, most of the time, I'm only an open-source consumer, not a contributor, by any measure.

But hey, you can't force people to contribute, you can't motivate people who don't have the motivation to contribute.

### 1.1 My Stories of Contributing to Open-Source Projects

I'm not always like that, though. I did contribute to open-source from time to time:

- There was this one time when I used Terraform to manage the Microsoft Azure cloud platform at work. I remember that back then, a new setting for a specific service was already live in their production, which we needed, which we could set the values for in the Azure web console. But since we are doing 100% infrastructure as code, manually logging in to a web console and clicking things would break our automated workflow. There was nothing I could do except to go to the Terraform Azure provider and contribute a little bit of code.
- There was another time I was told by the recruiters that CVs with open-source experience might be prioritized by some companies, so I decided to do a few things here and there to make my CV look better
- Yet another time, I was simply interested in a new piece of tech so I decided to learn it the open-source, the contributor way.

You might have already seen where I'm going with this, and you are doubtlessly right: _motivations vary (as much as people themselves vary.)_

### 1.2 Why Do People Contribute

People might contribute for completely different reasons:

- need a feature for that software for work
- want to learn something
- want to level up their CV
- ...

If Terraform fits my professional needs perfectly without any issue (well, most of the time it does), I don't have to contribute, and HashiCorp or Terraform community can't possibly sell me the idea that if I contribute today, maybe next time when I do meet an issue which nobody has fixed yet, I can fix it myself since I already knew how to do so.

If I choose to learn Rust by reading the official docs and trying it myself, any Rust project can't force me to learn Rust by contributing to their community.

So, the question "why do you contribute" doesn't matter: you can't control it. You can't control people's initial motivation to contribute. What triggers them? It's difficult to answer the question, not to mention to create an actionable plan out of it.

What you can control is how to _keep them motivated_ once they've started contributing.

But how?

This is the million-dollar question to be answered, and next, let's tackle that.

---

## 2 Keep'em Motivated

Let me cut straight to the chase: there are a few things you can do to keep your community members motivated.

### 2.1 Be Honest, Communicate Clearly

Explicitly state the "level of effort" required to contribute. How much time it's going to take? If you don't define these explicitly, they might guess, and they probably will have false expectations, which leads to frustration, or even the loss of trust. _Trust is a thing that is hard to gain but easy to lose._ If they are not clear about what they are getting into, they might not even contribute in the first place.

Elaborate, in every document and issue. Be as descriptive as possible. Tell the contributors what they need and what you are expecting. If not, you might get PRs that are not what you are looking for, you might discuss a lot in the issue, the contributors might get frustrated, and lose trust in the community.

Build a contributor ladder/progression path. It's like a career. Although it's not a company-employee relationship, you do ask them to contribute their time. More on this later.

Create a Roadmap. You need to let them know where you are going, and where they are going, and whether your goal aligns with theirs or not.

### 2.2 Lowering The Bars to Contribution

The reason behind this is extremely simple: if contributing is a pain in the ass, their motivation (no matter what it is) will disappear.

The goal is to make "contributing to your project" as easy, and as intuitive as humanly possible.

To achieve this, there are 3 action items that I can recommend:

**1 Write good documentation with details.**

- The docs should set the _right expectations_. This action item is related to section 2.1.
- State what needs to be done to create an issue. Searching existing issues to make sure there are no duplicated ones?
- State what needs to be done clearly when submitting a PR. Unit tests? Local test? Screenshot? Anything else?
- State the whole process in detail. When will the PR be reviewed? How does the review process work? When will it be released? Documenting all the details can smooth the whole contribution process.

**2 Minimize the required steps.**

- Write a "quick start" documentation: this is probably the very first one that contributors are going to read.
- State clearly what are the tools and dependencies.
- Automate the dependencies, if possible. This reduces one manual step.
- Set up the environment with automation, if possible. This also reduces one or even multiple manual steps.
- State clearly how to build/test the project.

**3 Good First Issues**

A great way to encourage new contributors is to prepare some issues that are suitable for new people to the project, and make those issues easy to find.

One way to achieve this is to use labels, and one of the most common labels for this purpose is probably the famous "good first issue."

But How do you prepare good first issues so that they encourage new people to participate? Here're some key takeaways?

- Low (read: no) barrier to entry: tasks labeled with "good first issue" should be something that any new contributor can handle without any advanced setup or knowledge.
- Provide context and detail: why is it needed, what background knowledge is a prerequisite, etc. Things like this should be cleared up explicitly. If the background knowledge is a bit intimidating, maybe also include a list of reading materials.
- Explain possible solution: if there is already a recommended solution (there should be, for a "good first issue",) explain it clearly, mention the expected result/behavior, and maybe even give some examples of similar implementations, so that new contributors have a reference.
- Codebase walkthrough: either provide a simple document, blog, or anything to that effect to walk them through your code base so that they can get started quickly and easily, or identify the code blocks that are relevant directly to the issue.
- Tests/docs: is there any test/doc related to this issue? If so, point it out as well, so that the new contributors know what else needs to be updated other than code. For tests, maybe there is already some kind of tests similar to the ones that need to be written. Point out similar tests so that first-time contributors have some references.

And other actions. The goal is to minimize the steps as much as possible.

### 2.3 The Human Element

So far, we've focused mainly on the technology part.

We've focused mainly on the tech part that we've completely forgotten about the human factor, and this could discourage people.

The personal touch is the most important factor; yet, it's often overlooked.

To place great attention to it, I decide to write it in the next chapter separately.

---

## 3 The Human Factor

The personal touch is the most important, yet often overlooked factor.

### 3.1 Recognize Contributors

Some small actions that you can do that serve as recognition:

Thank every single contributor publicly (especially new ones!) We do this frequently, most likely in finished pull requests, release notes, and contributor groups. Even in issues. The place where you do this or the format doesn't matter. What matters is that you make sure you convey this human touch.

Create a welcoming community, on purpose. You may have an unpleasant experience in communities, coding related or not. Not every community is created equally. They have different styles and ways to engage. But you can choose to go the extra mile and add that extra human touch to your community. Welcome new contributors who have joined the channel/group is a start. Try to reply to contributors' questions in great detail. There are literally thousands of TODOs. In short, be nice.

Host some events. Invite contributors to meet-ups and community meetings, maybe even invite them to give short speeches, to let them feel valued. 

Mentoring opportunities: either you mentor them (for example through online meetings to give them quick walkthroughs on how to contribute,) or allow them to be mentors for even newer contributors.

Last but not least, swag. The audience who are familiar with the "Silicon Valley" show should be familiar with this concept. It sounds silly, but it works. Give your contributors chances to show off, to feel ownership and belongingness.

### 3.2 Create Recognition Programs

Create some kind of recognition program.

It doesn't have to be some literal "programs" per se, but have it in mind about what you want to do to show the recognition.

For example, in one of my current open-source projects, we created [a section specifically on our website to celebrate any new contributor or member](https://www.devstream.io/community/contributor/contributors).

But hey, I didn't invent this. It would be arrogant beyond belief if I said I invented this. This is something the open-source community already took for granted. See another example [here](https://linkerd.io/community/heroes/).

For another example, you can even write blogs about your new contributors; invite them to write blogs on your project's official blog; invite them to join podcasts; etc.

### 3.3 Create a Contributor Growth Ladder

One of the motivations for many contributors is the "status in the project." If we give certain contributors the title of "member/reviewer/maintainer" etc., they will be motivated.

The contributor growth ladder tries to answer one simple question: how do I advance in this project?

But what exactly is a growth ladder?

Moving contributors up, as their contributions grow in quantity and quality. They will get more authority and responsibility. This is the ladder we are talking about. With a contributor growth ladder, they know what they will be "rewarded": greater authority in the project, more responsibility, etc.

With a growth ladder, contributors will also know exactly what they need to do to move up the ladder: becoming a member or even a maintainer isn't something vague and impossible.

We are humans after all, and humans are creatures of emotions. When the project and community grow bigger, we might lose track of all contributors. Sometimes, we tend to promote people who showed up more in the meetings but miss people who are on the other side of the globe but doing solid work. Having an explicitly defined career ladder could help in this kind of situation.

When creating a growth ladder, there are a few key things to document:

- Explicitly define measurable requirements. I.E., what needs to be done to reach what level. For example: "if you want to become a reviewer, you need to review more PRs." This is too vague. A better approach would be: "You need to review 5 PRs." Some people might not have time to do that, and that is fine, but some will say "just 5? I can do that" and they will be motivated.
- Privilege for each level. If they don't gain more authority and responsibility but only a "title," that doesn't seem to be enough motivation. It's like spiderman: _with great power comes great responsibility_.
- Process for approval. How to review? How to make sure we have equal chances? Document your process and make it unbiased.

### 3.4 Non-Code Contributions

So far, we have been mainly talking about "coders" types of contributors. But more often than not, non-code contributions are more important. Examples:

- writing, maintaining, translating documentation
- sharing their story about this project
- helping others on Slack channels and WeChat user groups
- helping to manage the communities

What's more, most maintainers are coders, who might have a bias towards non-code contributions; so we need to pay more attention here and make the pivot: non-code contributions are equally important, if not more than, code contributions.

### 3.5 Maintaining/Governance

People care about belonging to something. They want to be equal participants other than dictatorship. They want to be treated equally with respect.

And this is where formal, written governance kicks in: it proves that all contributors are equal participants; you won't be treated differently if you don't belong to the company that started this open-source project in the first place.

Imagine some users from another company already started using your product but then you decided to change your roadmap and your interest diverged from theirs. When such conflicting incidents happen, the contributors want to have a voice in these changes. Formal written governance makes contributors feel safe to contribute; you won't decide to take a 180-degree turn all of a sudden without a formal decision process. With this guarantee, they may invest more time in it, which means increased influence.

Even for independent contributors who don't use your project in any company, formal written governance would show fairness and respect to them. They'd feel they own the project, and of course, you would be much more likely to contribute much more to a project that you truly own.

But, you don't need to have a complicated set up right in the beginning. 

For starting projects, or, in the "sandbox" stage, a 2-level/3-level contributor growth ladder is more than enough. You won't need 10 levels if you have only 10 contributors, makes sense? And maybe you can have a short page of `CONTRIBUTING.md` doc. And maybe a document of "code of conduct".

For more mature projects, like in the "incubating" stages, you can have slightly more levels on the growth ladder; you can start building the maintainer council for governance, with more guides and notes

If you are graduating from a foundation, you can even operate your committee with formal elections, define more roles in docs/handbooks, create handbooks, create handbooks for new contributors, and have a committee to settle breaches of the code of conduct, etc.

---

## 4 No Need to Reinvent the Wheel

If you have followed this far, you probably would think building a community takes a lot of time and effort. You are right because it does.

However, you do not have to reinvent most of the aforementioned wheels. Refer to other open-source projects and communities and even foundations. They might have already got a few resources and templates to help you get started quickly.

For example, check out the CNCF maintainer website, where you can find helpful tips and suggestions which are all actionable. What's more, they've got many documentation templates that you might simply copy and adjust and use in your projects.

---

## Summary

Sorry that I put the TL;DR at the end, but this isn't a mistake, it's pretty much on purpose. Because unlike the "People Powered" book which is full of truth without any action item, this post is full of action items and explains why you need to do that. So, sorry for wasting your time read the whole thing first, but if you learned merely a small thing or two from my post, I'm more than satisfied.

Here's a quick "cheat sheet" for you to check:
- keep your contributors motivated and encouraged to contribute more, and level them up. This can be done via:
	- communication
	- lowered barriers
	- recognition
- create recognition program(s) (yep, you can have more than one)
- recognize, encourage and cultivate your non-code contributors
- use formal governance and contributor rules to lower the risk and difficulty, and governance should evolve with the stage of the project.
