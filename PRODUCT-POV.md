# Quarterstack — Product Point of View

## The Problem (as I see it)

PMs don't lack frameworks. Every PM knows RICE, ICE, MoSCoW. The actual failure mode in quarterly planning is context switching. You pull data from Amplitude, customer feedback from Slack, revenue signal from Sales, ticket counts from Support — then consolidate it all into a spreadsheet, apply a framework, debate trade-offs in a meeting, and produce a plan in a third tool. Each switch is cognitive load. By the time you have a plan, it's already stale.

## The Bet

**Collapse the entire workflow into one continuous surface where scoring, deciding, and planning happen together — not sequentially.**

Most tools separate "evaluate" from "decide" from "plan." You score features in one view, build a roadmap in another, and discuss trade-offs in a meeting. Quarterstack treats these as one fluid motion: features are pre-scored, the plan builds itself as you make decisions, and AI agents handle the grunt work of data collation and conflict detection. The PM's only job is judgment.

## Key Design Decisions

### 1. No framework selection step
**What:** We auto-apply RICE and show a "How scores work" tooltip. No framework picker.

**Why:** Asking a PM to choose between RICE, ICE, and MoSCoW before they've even started is an analytical choice that adds friction with zero value. The framework is infrastructure — it should be invisible. A "pick your framework" modal is a tool designed for tools, not for outcomes.

### 2. One scrollable surface, not tabs or steps
**What:** Backlog, cut line, and Gantt chart live on the same page. Scroll down = move through the workflow.

**Why:** Tabs and wizards create context switches. A PM adjusting a score needs to immediately see how it affects the plan. With tabs, that's two clicks and a mental mapping exercise. With one surface, cause and effect are visible simultaneously. This is the zero cognitive load principle — don't make the user hold state in their head.

### 3. The Cut Line as the hero interaction
**What:** A draggable divider that separates "this quarter" from "not this quarter." Everything above it auto-populates the Gantt. Everything below is parked.

**Why:** The single most important decision a PM makes during planning is: what's in, what's out. Not scores. Not frameworks. The cut. We made this the central, most visible, most tactile interaction. Drag it down to add features, drag it up to cut scope. The plan updates instantly. No "generate roadmap" button. The plan IS the list above the line.

### 4. Two specialized AI agents, not one generic chatbot
**What:** An Analyst agent (handles scores, data, context) and a PO agent (handles trade-offs, risks, capacity). User switches between them via tabs.

**Why:** A generic "AI assistant" is a blank canvas — the user has to figure out what to ask. Specialized agents have clear jobs. When you talk to the Analyst, you know you're asking about data. When you talk to the PO, you're asking about decisions. This maps to how real teams work: you don't ask the same person to pull data AND make the priority call. It also aligns directly with Tasket's "Agents as Peers" principle — agents as collaborators with distinct roles.

### 5. Gantt chart with parallel streams, not monthly columns
**What:** The quarterly plan renders as a Gantt with 2 parallel work streams across 12 weeks, bars sized by effort.

**Why:** The initial version used 3 equal monthly columns. That's a calendar, not a plan. It doesn't account for effort or parallelism. The Gantt shows reality: which features can run concurrently, how much of the quarter they consume, and whether you're over capacity. A PM glancing at it knows instantly if the plan is feasible. No mental math needed.

### 6. Pre-enriched features with source links
**What:** Every feature card arrives with scores pre-filled, a data citation (e.g., "12 support tickets, mentioned in 3 renewal calls"), and clickable source links (Slack threads, dashboards, meeting notes).

**Why:** The biggest time sink in planning isn't scoring — it's gathering context. "Where did this request come from? How many customers asked? What did the data say?" The Analyst agent has already done this work. The PM reviews and adjusts, rather than starting from scratch. Source links let them verify without leaving the tool.

## What We Excluded (and Why)

| Excluded | Why |
|----------|-----|
| **Feature ingestion pipeline** | Assignment scoped it out. But the design assumes features arrive pre-enriched — the Analyst agent's job is to show its work, not require the PM to do the intake. |
| **Export / sharing** | Assignment scoped it out. The plan lives in the tool. |
| **Team collaboration / comments** | This is a single-PM planning tool, not a team debate platform. Adding comments, mentions, and threads would triple the UI surface for a use case that's better served by the agents. You discuss with the AI, not with teammates in this flow. |
| **Multi-quarter comparison** | Scope creep. One quarter at a time. If you need to compare Q2 vs Q3, that's a reporting tool, not a planning tool. |
| **Custom framework builder** | We support RICE with adjustable weights via sliders. Building a full "create your own framework" editor serves maybe 5% of PMs and violates the zero cognitive load principle. |
| **Sprint-level capacity planning** | This is quarterly planning — the unit is weeks, not story points. Detailed sprint planning is a different tool for a different moment. The Gantt gives "roughly feasible" which is what a quarterly plan needs. |
| **Notifications / reminders** | Out of scope for a planning session tool. This is a "sit down and plan" experience, not a "check in daily" dashboard. |

## Design for Delight Alignment

| Principle | How we applied it |
|-----------|------------------|
| **Zero Cognitive Load** | No framework picker. Scores pre-filled. Plan auto-generates. The PM makes judgment calls, not data entry. |
| **Smart Defaults** | Cut line starts at a sensible position. Scores are pre-filled by the Analyst. New features get default scores. Theme and source dropdowns pre-selected. |
| **Progressive Disclosure** | Collapsed cards show only title + score. Expand to see data, sources, sliders. The Gantt only appears below the backlog — you see it when you're ready. |
| **One Page, One Context** | Single scrollable surface. No tabs for the main workflow. No modals except the add form. |
| **Instant Feedback** | Drag the cut line — plan updates instantly. Adjust a slider — score pulses and list reorders. Delete a card — slide-out animation + undo toast. |
| **Fewer Words** | Labels are "Impact" not "Estimated Business Impact." Cut line says "8 in, 6 out" not "You have selected 8 features for inclusion in the quarterly plan." |
| **Micro-interactions** | Score pulse on change. Gantt bars animate in with stagger. Confetti when plan goes from over-capacity to fits. Card slide-out on delete. Typing indicator in chat. |
| **Familiar Mental Models** | Drag to reorder (Trello). Sliders for scoring (any form). Chat sidebar (Slack/ChatGPT). Gantt chart (every PM tool). Nothing requires learning. |
| **Purpose-built Design** | The cut line is not a standard UI pattern — it's designed specifically for the "what's in / what's out" decision. Dragging a line is more intuitive than checkboxes or drag-to-bucket. |

## If I Had More Time

1. **Agent actions that modify the board.** Right now agents give advice. Next step: "Move all infra features to Month 2" in the chat, and it actually happens. The PO agent becomes a pair-planning partner, not just an advisor.

2. **Dependency visualization.** Draw lines between features that depend on each other. The Gantt would auto-sequence them so dependent features never start before their blockers finish. The PO agent would flag circular dependencies.

3. **Scenario comparison.** "What if we cut Custom Dashboards and add Slack integration instead?" Save two versions of the plan side-by-side. Compare total effort, theme coverage, and risk profile. Make the trade-off visual, not verbal.
