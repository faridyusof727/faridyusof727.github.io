+++
date = '2026-01-04T12:10:00+08:00'
title = 'Early Feedback Loop: Working Smart on Frontend Development'
description = 'A practical approach to getting visual approval before code review saves time for everyone.'
+++

![early-feedback](/early-feedback.png)

## Early Feedback Loop

At most places I've worked before, we were conditioned to complete tasks
entirely - PR, deploy to stage or testing environment - and only then
would we get feedback from the "Product Team" / "QA" team.

I think this is incredibly wasteful, especially for things involving UI/UX and
design. I'd often get feedback like:

* Color doesn't look right (change the color)
* Component position is off
* Animation doesn't fit
* etc

Imagine how much time wasted preparing the PR, waiting for code review, fixing
conflicts, deploying to staging, then only finding out "oh this color isn't
nice, change red to blue."

Stupid, right?

**This is the situation when a company doesn't have a proper design team.**
When there's no Figma link, no design specs, requirements are just verbal or
in vague Jira descriptions. You're forced to improvise, guess what the product
owner wants. Then deploy only to find out you got it wrong.

If a company has a design team that prepares Figma designs first in the task,
there's no issue. Everything's clear - spacing, colors, typography, interaction
states all specified. Just implement according to spec. When there's a proper
design system, work becomes predictable.

But reality? Many companies don't have that luxury. Especially startups or
companies where the product team assumes developers can design too. Or worse,
there's design but it's half-baked - static mockups but interaction states are
all unclear. What about loading state? Error state? Empty state? You have to
figure it all out yourself.

So I started a simple practice: screenshot first, video first, get approval
first, then push code. This saves my time, saves reviewer time, saves
everyone's time. Product owner is happy because they see results quickly.
Engineers are happy because they don't have to rework multiple times.

I usually record short videos, 30 seconds to a minute. Show the flow, show
interactions, show responsiveness. Send it on Slack or Teams. Within an hour or
two, I get feedback. If something needs changing, change it right then, haven't
even committed yet. Easy.

Separating visual approval from technical review is a real game changer. Once
the product owner is okay with the UI, then submit the PR to focus on code
quality. Reviewers can focus on "is this maintainable?" instead of "should this
button be 2px to the left?"

I learned this practice after getting burned a few times. One time, I spent
almost a week building a complex form with validation, animations, everything.
Deployed to staging, got feedback "actually we want it simpler, remove most of
these fields." That week could've been saved if I'd shown a wireframe or quick
prototype first.

Simple practice, but huge impact. Especially when you work in an environment
without a proper design process. It's about working smart, not just working hard.
