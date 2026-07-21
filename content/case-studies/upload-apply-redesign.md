---
title: "Reimagining Upload & Apply — Monster and Zety"
date: 2026-07-15
description: "Leading the AI generation workstream for a ground-up redesign of the resume upload & apply experience: 12 net-new AI-first APIs and an inference layer that turned a content playground into a guided product."
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

## The problem

The old upload flow accepted your resume and handed you a toolbox. The content suggestions were well written, but generic by construction — the same suggestions for everyone. A nurse with twelve years of experience and a college senior with one internship saw the product behave identically.

What was missing wasn't quality. It was a point of view: nothing in the flow said "given who you are and where you've been, this is the best version of this section for you."

## The approach: infer first, generate second

The foundational decision was that no content generation should happen without understanding who it's for. So the first thing we built wasn't a generator — it was an **Inferred Context Layer**: an internal service that reads a user's resume and produces a structured profile of the dimensions along which good resume advice actually diverges.

An LLM sits at the core, but the layer is wrapped in structural formalism — constrained outputs, deterministic post-processing — so the same resume yields consistent context across runs. Every downstream API takes that context as an input, which means personalization comes from one coherent understanding of the user rather than twelve APIs making twelve independent guesses.

From there, each resume section follows the same pattern: generate a best guess before the user touches anything, then offer AI-powered tools to refine it.

The work also coincided with a platform-wide model migration, which I ran as a structured evaluation — an atomic rubric scored by a mix of deterministic checks and LLM-as-judge, calibrated against subject-matter experts rather than trusted on its own. That harness is now standing infrastructure; the next migration starts from a rubric instead of a blank page.

## What I took from it

Personalization is an inference problem before it's a generation problem. The temptation is to prompt your way to it inside each feature. Centralizing "who is this user" into one rigorously structured layer is what made twelve APIs coherent instead of twelve clever.