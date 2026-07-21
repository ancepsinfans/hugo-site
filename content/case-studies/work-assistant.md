---
title: "Work Assistant — A Personal Chief-of-Staff Agent"
date: 2026-07-20
description: "A multi-source agent that collapses duplicated work signals into one prioritized picture — and runs a second pass to find what should be there but isn't."
theme: Toha
menu:
  sidebar:
    name: "Work Assistant"
    identifier: work-assistant
    parent: case-studies
    weight: 30
---

## Snapshot

**Role:** Designed, built, and maintain it — this is a personal project, not a team deliverable
**Stack:** Python, SQLite, sentence-transformers (local embeddings), provider-agnostic LLM layer (Anthropic / OpenAI / Ollama), launchd + Task Scheduler
**Status:** Running four times a weekday on my machine
**Repo:** [github.com/ancepsinfans/work-assistant](https://github.com/ancepsinfans/work-assistant) — built for myself; packaged as a forkable template. Swap the prompt templates and domain rules, point it at your own vault.

## The problem: one event, five todos

Modern product work generates the same signal in five places. A ticket moves, an email fires, someone Slacks about it, a Confluence page gets edited, and it surfaces again in a standup transcript. That's one event — but every tool you own presents it as a separate thing demanding separate attention.

The obvious fix is aggregation, and the obvious fix is wrong. Pulling five feeds into one feed produces a longer feed. What I wanted was *collapse*: deduplicate across sources, decide what actually needs me, and hold enough context that tomorrow's run starts smarter than today's.

## What it does

Work Assistant isn't a chatbot you visit. It's a scheduled background process with two on-demand companions:

- **`main.py`** runs four times a weekday — fetches every enabled source since its last checkpoint, pre-processes long content, investigates standing questions, synthesizes a deduplicated task list and tiered memory, then writes it all back to an Obsidian vault.
- **`ask.py`** answers a single question against everything it knows, from the terminal or a Raycast hotkey. Built for the hallway conversation where you need "what did we decide about X?" without opening five tabs.
- **`meeting_brief.py`** polls the calendar every five minutes and writes a pre-meeting brief — attendee context, semantically related past decisions, open tasks mentioning attendees — before the meeting starts.

Obsidian is the human-readable surface. SQLite is operational state: checkpoints, task rows, embeddings, metrics. That separation is what makes the whole thing forkable.

## The design idea: build for absence, not just presence

The pass I'm most attached to isn't the synthesis pass. It's the one that runs after it.

The **absence sweep** takes the task list the main pass just produced, plus rosters of everyone who appeared in Slack, email, and meetings, and asks a different question: what *should* be here and isn't? Commitments without follow-through. Expected updates that never arrived. Tickets that have gone quiet. Threads where someone asked you something and the conversation simply stopped.

Nothing in an inbox tells you about the email that didn't come. Aggregators are structurally incapable of surfacing this, because they can only rank what exists. Getting it required treating negative space as a first-class output — a separate prompt, a separate pass, its own tasks flowing into the same reconciliation.

It's the same instinct that shaped my work on inferred user context at BOLD: the interesting design question is usually about the boundary of what a system knows, not the volume of what it collects.

## Architecture decisions worth defending

**Memory as tiers, not history.** Five markdown files — daily, weekly, sprintly, monthly, quarterly — that the agent rewrites on its own cadence. Daily updates every run; weekly at the last run of the day; sprintly on Friday; quarterly at quarter-end. The rule the prompts enforce is *contextualize downward, synthesize upward*: daily memory references quarterly stakes, quarterly memory compresses granular detail into patterns. Each run therefore begins with compressed analytical context instead of re-reading three weeks of Slack.

**Self-healing schedules.** Calendar-triggered work is fragile — laptops sleep, VPNs drop, the 4:30 PM Friday run fails at exactly the wrong moment. Every tier carries a staleness threshold alongside its trigger, so a missed window repairs itself on the next successful run instead of silently leaving a gap in the record. This is unglamorous and it's the difference between a demo and something you trust.

**A feedback loop that respects the human.** Tasks live in SQLite as the source of truth, but render to a markdown file you edit. Each run starts by reading which boxes you checked and resolving those rows *before* synthesis, so the model never re-surfaces work you've already dismissed. The agent proposes; you dispose; the agent remembers that you disposed. Day-to-day triage and capture live in [TaskFlow](https://github.com/ancepsinfans/taskflow), a companion self-hosted task manager on the same stack — Work Assistant handles synthesis and memory; TaskFlow handles interactive prioritization.

**Local where local wins.** Embeddings always run locally (`all-mpnet-base-v2`, brute-force cosine similarity in numpy) — appropriate for thousands of entries, no API dependency, no cost per query. Pre-processing passes run fine on a local model; the main synthesis pass benefits from a stronger cloud model because it emits large structured JSON. Three providers behind one factory means the whole thing can also run fully offline if your situation requires it.

**Spend nothing on quiet days.** If there's no new source data, no unanswered standing questions, and no memory tier due, the run exits before it ever calls a model.

**Standing questions, actively investigated.** A markdown checklist in the vault — "has the team responded to my API proposal?" — gets read at the top of every run. Unchecked items become parallel searches across every source plus the semantic index, and the findings go into the synthesis prompt so the model can judge answered, partial, or still silent. It's the ten minutes of morning check-the-threads I was doing manually, done before I sit down.

## Packaging it

I built this for myself, and I use it every working day. Making it forkable was a separate discipline from making it work: a guided setup that walks a new user through provider choice, credentials, and vault creation; a Windows port with its own installer and scheduler path; templated prompts and domain rules so behavior is configurable without touching Python; and documentation good enough that nobody has to ask me how it works.

That transition — from a thing that runs on my machine to a thing that could run on someone else's — turned out to be the most PM-shaped part of the project.