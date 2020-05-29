---
layout: post
title: "Finding a BFF in Zero Bug Balance"
---

I'm a software engineer. In my department, we have a metric called **Zero Bug Balance** intended to increase our software quality.

Periodically, we:

* Count bugs found
* Count bugs fixed
* Apply a top secret formula: `bug_balance[this_time] = bugs_found - bugs_fixed + bug_balance[last_time]`
* If `bug_balance[this_time] > 0`, that's kind of bad.
* If `bug_balance[this_time] > bug_balance[last_time]`, that's bad for real.

This is a convenient metric that management uses to gauge how each project is going, but it could be improved.

## Encouraging an unhealthy work culture

[Goodhart's Law](https://en.wikipedia.org/wiki/Goodhart%27s_law) states:

> "When a measure becomes a target, it ceases to be a good measure."

Zero Bug Balance as a scalar metric promotes an unhealthy work culture.

With Zero Bug Balance...
* reporting bugs looks bad
* fixing bugs looks good
* keeping bugs looks bad

To our department's credit, nothing very bad happens if our bug balance is nonzero, aside from the public shame of admitting we created more than zero bugs (sometimes a lot more).

The shame largely works--we've felt it when filing a bug. Unfortunately, I have been cautioned about labeling issues as "bugs" because we're chasing Zero Bug Balance, and `last_time` we had bad numbers. Alternatives have included filing a card without _labeling_ it as a bug, or just mentally noting its existence and forgetting it until it happens again.

By shaming teams for reporting bugs, Zero Bug Balance can lose its accuracy in the unhealthy work environment it promotes.

## Disregard for bug severity

I have an arsenal of negative experiences with  [SAFe](https://en.wikipedia.org/wiki/Scaled_agile_framework), but I'll share something _good_ from my time with it: we learned risk assessment 101. Issues were cast onto a 2-dimensional risk matrix I still consider when defining bug **severity**:

* **probability**: likelihood or frequency that a bug occurs.
* **impact**: how awful things get because of the bug.

Discerning severity quantifies the fear it strikes into each engineer's heart. Left to any team that values sleep, prioritizing fixes for bugs scary enough (sufficient `probability * impact`) to keep them up at night will occur naturally.

Zero Bug Balance counts all bugs equally scary, from annoying afterthoughts to nightmares. This isn't necessarily bad, but the implications of allowing none may be.

## Limiting teams' ability to use technical debt

It would be a dream to keep no bugs around. However, here in reality, teams must weigh the opportunity cost to solve a bug, considering other priorities. [Erik Bernhardsson describes this scenario, as seen by outsiders:](https://erikbern.com/2020/03/10/never-attribute-to-stupidity-that-which-is-adequately-explained-by-opportunity-cost.html)

> Why is _bug Z_ still present? Hasn't it been known for a really long time? I don't understand why they aren't fixing it?

And his answer:

> Of course, why these things never happened is that _something else was more important._

A visual bug in a UI probably matters less than a data corruption bug in an API. Similarly, a bug in a component may not be worth fixing if a new component will replace it entirely. Or perhaps a bug is worth fixing _sometime_, except the person representing the entire [bus factor](https://en.wikipedia.org/wiki/Bus_factor) for that part is on vacation.

In these situations, the team may accept the technical debt of solving the low-severity bugs later. Allowing some technical debt is good: it affords the option to push higher-priority features or fixes.

Zero Bug Balance does not account for _acceptably_ low-severity bugs, which disregards weighing opportunity cost, and discourages the team from leveraging technical debt to prioritize shipping features or improve elsewhere.

## Zero Bug Bounce is a measure worth learning from

Microsoft's Zero Bug Bounce is a state of product maturity that teams strive for, described in [Mike Torres' opening paragraph in his article applying it to life](http://www.refocuser.com/2009/04/bouncing-at-zero-zbb-in-life/):

> ... all active bugs in the software have been looked at and either punted or fixed – and the team’s fix rate (or the rate at which they’re able to fix bugs) is greater than the team’s incoming rate (or the rate at which new bugs are being opened).

Zero Bug Bounce differs from Zero Bug Balance in that **punting a bug** (deferring a fix until later) counts as fixing it, and focuses on bug-finding rate relative to team capacity. However, Zero Bug Bounce is only meant to account for _new_ bugs, and is unaffected by shrinking a running bug balance.

## Solving with Bugs Found and Fixed (BFF)

I propose a friendlier solution to Zero Bug Balance that I'm dubbing **Bugs Found and Fixed**, or **BFF**.

Recall Zero Bug Balance's formula:

```python
bug_balance[this_time] = bugs_found - bugs_fixed + bug_balance[last_time]
```

Suppose we make an operator more positive, and stopped caring about bug balances:

```python
bff = bugs_found + bugs_fixed
```

This _absolutely groundbreaking_ formula is actually a better alternative to Zero Bug Balance, and even Zero Bug Bounce:

* Culturally, _finding_ a bug is as rewarding as _fixing_ (closing) a bug.
* It allows teams to consider opportunity cost and punt a less-severe bug as technical debt to pay down later.
* Fixing a bug of any age, even punted ones, counts toward BFF.
* BFF reflects changes to bug balance, obsoleting bug balance reports.
* BFF is intentionally still a single, convenient number that anyone can scramble to calculate four minutes before the monthly reports presentation starts.

Admittedly, BFF alone can be gamed by a bored engineer filing many small bugs in place of one, but a picture paints itself when combined with other metrics:

* If BFF is steady but support requests are high, the team may not be dedicating time to product improvements.
* If BFF skyrockets while deployment frequency or feature development slows, the team may be paying down technical debt.
* If BFF stalls, uptime is awful, and deployment frequency is low, you may have bigger problems than deciding how to count bugs.
* And if the team sleeps well and BFF is steady, you either have a mature product or no users.

At Comcast, our department is focused on better delivery. This starts with a healthy culture, and choosing what we measure plays into that. Metrics like uptime, deployment frequency, mean time to recovery, and how much sleep each team lost at night fearing an emergency page can be supplemented by counting Bugs Found and Fixed instead of striving for the intolerance of Zero Bug Balance.

Plus, who wouldn't want a good BFF?
