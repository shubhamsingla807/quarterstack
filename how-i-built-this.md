# How I Built Quarterstack

## How I Read the Brief

The brief says "quarterly planning & prioritization tool for PMs." Most people would read that and build a RICE scoring table with a Kanban board. That's the obvious answer.

I read it differently. The brief specifically says: PMs pull data from multiple systems, consolidate into spreadsheets, apply frameworks, produce a plan. That's 4 context switches before anything gets decided. The problem isn't "we don't have a framework." Every PM knows RICE. The problem is the process takes too long because information lives everywhere and decisions happen in meetings, not in the tool.

So I framed the whole thing around one question: how fast can a PM go from chaos to clarity?

## The Core Bet

Collapse scoring, deciding, and planning into one continuous surface. Not three views. Not tabs. Not a wizard. One page where you scroll from backlog to plan, and the plan builds itself as you make decisions.

This meant killing a few things most people would include:
- No framework selection step. RICE is auto-applied. The framework is infrastructure, not a feature.
- No separate "generate roadmap" button. The plan IS the list above the cut line.
- No settings, no config, no onboarding flow. You open it and start deciding.

## How I Arrived at the Key Decisions

**The Cut Line.** I kept asking myself: what's the single most important thing a PM does during planning? It's not scoring. It's deciding what's in and what's out. That's the cut. So I made it the most visible, most tactile thing on the page. A draggable line. Everything above ships this quarter, everything below waits. The plan section below it updates live.

**Two AI Agents, Not One.** My first instinct was a single chat sidebar. But I thought about how planning actually works in teams. You don't ask the same person for data AND for priority calls. The analyst pulls numbers, the product owner makes trade-offs. So I split it: an Analyst agent that handles scores, data citations, and context. A PO agent that handles conflicts, capacity, and "what if we swap X for Y" questions. Each one has a clear job. You know what to ask each of them.

**Gantt with Parallel Streams.** The first version had three monthly columns (Jul, Aug, Sep) with features listed under each. Looked clean but was useless. It didn't account for effort or parallel work. A 4-week feature and a 1-week feature got the same visual weight. So I replaced it with a proper Gantt: 2 work streams, 12-week grid, bars sized by effort. Now you can actually see if the plan is feasible at a glance.

**Source Links on Every Card.** During planning, the biggest time sink isn't scoring. It's "where did this request come from? How many customers asked? What did the data say?" I added source links (Slack threads, dashboards, meeting notes) on every feature card so the PM can verify without leaving the tool. The Analyst agent pre-fills these, the PM reviews.

## Iterations

The first version was functional but rough. Here's what I changed and why:

**v1 to v2: Killed the framework picker.** Had a dropdown with RICE, ICE, MoSCoW, Custom. Realized it was an analytical choice before the PM even started. That's friction. Removed it, auto-applied RICE, added a small "How scores work" tooltip for anyone curious.

**v2 to v3: Replaced monthly columns with Gantt.** Three columns looked like a calendar, not a plan. The Gantt with parallel streams showed actual feasibility. Added a capacity summary row at the bottom.

**v3 to v4: Redesigned the agent sidebar.** Initially the agent auto-switched based on scroll position (Analyst when viewing features, PO when viewing the plan). Tested it and it was confusing. You couldn't tell which agent you were talking to or why it changed. Replaced with explicit tabs: click Analyst or PO. Each tab has a one-line description of what that agent does. Much clearer.

**v4 to v5: Added source links, undo on delete, inline editing.** These came from thinking about edge cases. What if a PM deletes a feature by accident? Undo toast. What if they want to rename a feature during planning? Inline title editing. What if they add a new idea mid-session? Add form with source linking.

**v5 to v6: Micro-interactions and sound.** Added subtle audio feedback on key moments: a snap when the cut line drops, a pop when you add a feature, a whoosh on delete, and a C-E-G chime with confetti when the plan first fits within capacity. These are quiet, short (under 200ms), and only fire on moments that matter. Not on every click.

## Tools I Used

- **Claude Code** for prototyping. Same way someone would use Lovable or Bolt, but I prefer working in code directly because I can control the details. The prototype is a single HTML file with Tailwind CSS and vanilla JS. No build step, deploys straight to GitHub Pages.
- **Brainstorming with Claude** to pressure-test my product decisions. I'd lay out my thinking and use it as a sounding board. "Does this make sense? What am I missing? What would a PM actually want here?" Similar to how I'd bounce ideas off a colleague.
- **GitHub Pages** for hosting. Free, fast, no setup.

## What I Learned

The biggest lesson: the obvious answer (scoring table + roadmap) is almost never the right answer for a case study. The brief explicitly said "most vibe coding tools can produce something that works with the right prompt." They're not testing whether I can build a table. They're testing whether I have a point of view about how PMs should plan.

My point of view: planning tools should reduce decisions, not add them. Every dropdown, every config option, every extra step is cognitive load. The best planning tool is one where the PM opens it, sees their backlog pre-scored, drags a line, and walks away with a plan.

## Links

- **Prototype:** https://shubhamsingla807.github.io/quarterstack/
- **Product POV:** https://shubhamsingla807.github.io/quarterstack/product-pov.html
- **NSM & Events:** https://shubhamsingla807.github.io/quarterstack/nsm-and-events.html
- **Repo:** https://github.com/shubhamsingla807/quarterstack
