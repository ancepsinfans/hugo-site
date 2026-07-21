---
title: "Reimagining Upload & Apply — Monster and Zety"
date: 2026-07-15
description: "Leading the AI generation workstream for a ground-up redesign of the resume upload & apply experience: 12 net-new AI-first APIs, a platform-wide model migration, and an inference layer that turned a content playground into a guided product."
theme: Toha
menu:
  sidebar:
    name: "Upload & Apply Redesign"
    identifier: upload-apply-redesign
    parent: case-studies
    weight: 10
---

## Snapshot

| | |
|---|---|
| **Role** | Product Manager, AI Content Platform — led the AI generation (backend) workstream |
| **Scope** | 12 net-new AI-first APIs across Monster and Zety |
| **Timeline** | Mid-April 2026 planning → first-half-July launch, ahead of schedule |
| **Early results** | ~8% conversion lift (first full analytics review pending) |

## The problem: a playground with no point of view

The old upload flow accepted your resume and handed you a toolbox. Static content suggestions — professionally written, genuinely good — but generic by construction, because they were the same suggestions for everyone. A nurse with twelve years of experience and a college senior with one internship saw the product behave identically.

What was missing wasn't content quality. It was *guidance*: nothing in the flow said "given who you are and where you've been, this is the best version of this section for you." Users were left to assemble their own resume improvement out of parts, which is precisely the job they came to us to avoid.

The redesign inverted this. Instead of a toolbox, the product now leads with an opinion — our best guess at each section, generated for this specific user — and then offers AI-powered tools to refine from there. Getting to that opinion is what the backend work was about.

## Architecture: infer first, generate second

The foundational decision was that no content generation should happen without understanding who it's for. So the first API we built wasn't a generator at all — it was the **Inferred Context Layer (ICL)**: an internal service that reads the user's resume and behavior to date and produces a structured profile. Industry. Career-switcher signals. Flags for thin resumes, gig work, blue-collar backgrounds — the dimensions along which "good resume advice" actually diverges.

The signals are carefully architected rather than free-form. An LLM sits at the core, but the layer is wrapped in structural formalism — constrained outputs, deterministic post-processing — so the same resume produces consistent context across runs. That consistency is what makes the layer safe to build on: every downstream API takes ICL output plus the resume as input, which means personalization comes from a single, coherent understanding of the user instead of twelve APIs making twelve independent guesses.

On top of that foundation, each major resume section follows a two-stage pattern:

**Stage one: the flagship generation.** Our best-guess version of the section — a summary written for this user's actual trajectory, a skills list already categorized and prioritized — produced before the user has touched anything.

**Stage two: AI-powered refinement.** On the edit page, tools that use the same context: summaries re-targeted toward jobs we think the user would be strong in; automated suggestions for converting duties into measurable impact statements; and my favorite of the set, an AI-powered skills search — the user types a term, and instead of dictionary lookup, we generate a complementary set of skills aligned to both the search intent and the user's inferred profile, with semantic-duplication guards so "team leadership" doesn't come back when "people management" is already on the list. Because every suggestion carries backend priority and category labels, accepting a skill places it in the right position in the list automatically. Selection is one click; the information architecture is already handled.

## The model evaluation: calibrate the judges, then trust them

The redesign coincided with a platform-wide model migration, which I ran as a structured evaluation rather than a vibes-based upgrade.

The candidate set covered budget and flagship tiers across three providers, and for flagship models, multiple levels of reasoning effort. The scoring machinery had three layers:

1. **An atomic rubric** — 25+ granular checks per output. Deterministic checks (structure, constraints, banned patterns) scored in Python; qualitative checks scored by LLM-as-judge, with judges drawn from multiple providers to avoid self-preference bias.
2. **SMEs grading alongside the judges** on the same outputs, so we could measure judge-human agreement per check.
3. **A meta-evaluation of the judges themselves** — SMEs auditing judge verdicts directly.

The point of layers two and three: never blindly trust the judge. The goal was to calibrate automated grading until it reliably reproduced our SMEs' sense of *good*, at which point it could scale where humans can't.

Two findings shaped the outcome. First, for content generation, low reasoning effort won — higher effort added latency without adding quality users would ever perceive. Second, when we plotted the candidates on quality and latency (with cost tracked as a constraint), the winner was clear on those two axes rather than on price. We migrated the platform accordingly, and the evaluation harness is now standing infrastructure — the next migration starts from a rubric, not a blank page.

## Shipping with everything in flight

The genuinely hard part wasn't the architecture — it was that nothing held still. Backend, front-end, design, and content were all in motion simultaneously, which meant requirements shifted continuously in every direction.

That turned my job into three overlapping negotiations: representing actual backend capability to teams designing against it; anticipating requests that hadn't been made yet but predictably would be; and — the part that mattered most — architecting for the changes I could see coming, so that when they arrived they were parameter changes, not re-architecture. The ICL is itself the clearest example: a centralized context layer meant that when a front-end team needed a new personalization behavior mid-flight, the answer was usually "the context already supports that" rather than "that's a new pipeline."

We launched in the first half of July, ahead of schedule, across both Monster and Zety.

## Early results and what's next

Early post-launch data shows roughly an 8% conversion lift, with the first comprehensive analytics review still ahead — I'll update this page when those numbers land. Beyond the metric, the durable outputs are structural: an inference layer every future feature can build on, a calibrated evaluation harness that makes model decisions repeatable, and standardized prompt architecture across teams.

## What I'd tell another PM

**Personalization is an inference problem before it's a generation problem.** The temptation is to prompt your way to personalization inside each feature. Centralizing "who is this user" into one rigorously structured layer made twelve APIs coherent instead of twelve clever.

**Evals are a calibration exercise, not an automation exercise.** LLM-as-judge scales; SME judgment is ground truth. The work is closing the gap between them — after that, you get both scale and trust.

**When requirements can't be frozen, buy flexibility deliberately.** In a fully parallel program, the cheapest way to absorb change is architecture that anticipated it. Some of the best decisions in this project were things we built slightly more general than the spec demanded — on purpose.