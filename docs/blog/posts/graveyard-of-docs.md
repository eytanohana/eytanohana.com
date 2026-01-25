---
title: A Graveyard of Docs
description: My take on modern docs systems
---

# A Graveyard of Docs

*January 25, 2026*

<figure markdown="span">
    ![A Graveyard of Docs](../../assets/blog/grave-of-docs.png)
</figure>

You ask a coworker, "hey, support says this service is acting weird - is there any documentation for it?"

They send you a link to the page. You open it and the first thing you see, right at the top.  
**"Last Edited: 3 years ago."**

That timestamp tells you something important about the system that produced this documentation.
Not just that it hasn't been updated recently, but that no one has been forced to notice that it hasn't been updated.

There's no signal when it drifts out of date. No feedback loop pulling it back towards reality.

You haven't read a single sentence, but already a quiet decision has been made.
The page is no longer authoritative. At best, it might be directionally useful. At worst, actively misleading.

So, before the content even has a chance, trust is already lost.

## Why it happens

Are people just lazy? This pattern is so common it would be harsh, and itself lazy, to apply that explanation across the board.
Even in environments full of capable, well-intentioned people, internal documentation tends to age quietly and lose trust.

That consistency suggests the issue isn’t effort or discipline, but structure.

To understand why documentation so often becomes untrustworthy, it helps to stop thinking of it as a collection of pages
and start thinking of it as a system. One designed with very few signals when it begins to fail.

## Documentation as a System

Any system can be understood by what it rewards, what it detects, and what happens when it fails. Internal documentation is no exception.
Docs are usually written at moments of change: launches, handoffs, incidents, onboarding — but once created, they enter a system with
very little feedback about whether they remain accurate or useful.

The core failure mode is simple: documentation does not break when it is wrong. There is no alert when a page drifts
out of date, no tests that fail when reality changes, and no visible signal when trust erodes.

> Incorrect documentation can live indefinitely, "quietly filling up the graveyard."

The system rewards creation over maintenance. Writing a doc is visible and finite; maintaining one is ongoing and largely invisible.
Small updates rarely feel urgent, and deleting obsolete pages can feel risky. Over time, the system selects for new documentation
rather than accurate documentation.

Systems evolve continuously and when the documentation is decoupled from them, correctness becomes a matter of discipline rather than inevitability.

Finally, most internal documentation has no natural reader. People don’t browse docs proactively — they arrive when something
is already confusing or broken. In that context, even minor signs of staleness are enough to collapse trust before the content has a chance.

The result is predictable. Documentation ages quietly, trust erodes early, and teams learn to route around the docs instead of relying on them.
What looks like neglect is often just the system behaving as designed.

## Working Around the Docs

When documentation can’t be trusted, knowledge naturally concentrates in people. “Reach out to X, they understand Y” becomes the norm, 
and informal ownership replaces written systems. It isn’t negligence, it’s adaptation. Asking a person provides context, feedback, 
and confidence that static documentation cannot.

Over time, that knowledge is handed down informally as people join and leave the organization. What survives is how 
the system behaves, not why it behaves that way. Decisions, tradeoffs, and historical constraints fade, leaving behind 
patterns that are followed but no longer understood.

Eventually, someone needs to make a change and there is no longer a clear expert to ask. At that point, the system 
itself becomes the documentation. Code is read, logs are traced, edge cases are rediscovered, and understanding is 
rebuilt from first principles until a new person becomes “the one who knows,” and the cycle repeats.

## The Hidden Cost

Routing around documentation keeps work moving, but it carries a cost that’s easy to miss. When knowledge lives primarily
in people, every question becomes an interruption, and every answer depends on availability. What works for a small team under
low load scales poorly as systems and organizations grow.

Over time, knowledge becomes brittle. Onboarding slows because understanding must be transferred person by person.
Incidents rely on memory instead of shared reference points. Changes become riskier, not because the system is complex,
but because its reasoning is no longer visible.

None of this is accidental. It's the predictable outcome of a static documentation system that provides no feedback when it drifts out of date.
The organization pays the price not all at once, but gradually, in coordination overhead, repeated rediscovery, and lost confidence.

## Designing for Trust

Documentation rarely fails because people don’t care enough to maintain it. More often, it fails because the surrounding systems
provide no signals when trust begins to erode. In the absence of feedback, decay is invisible, and invisible problems rarely get fixed.

Designing for trustworthy documentation means treating it less like an archive and more like an interface. Interfaces earn trust
through clear signals, tight coupling to reality, and visible failure when assumptions break. Documentation that participates in
the systems it describes, rather than sitting beside them, has a chance to remain relevant.

The goal isn’t more documentation, or even better-written documentation. It’s documentation that makes its own state
legible: when it is current, when it is drifting, and when it should no longer be trusted. Without that, the outcome is predictable.
With it, trust becomes something the system can support rather than something people have to guess at.
