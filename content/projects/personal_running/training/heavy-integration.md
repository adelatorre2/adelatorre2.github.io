---
title: "Heavy Integration Notes"
date: 2026-06-24
summary: "Notes and ideas for connecting Heavy strength training data with my running training log."
categories: ["personal-running"]
tags: ["strength", "heavy", "api", "training-log"]
build:
  list: never
---

## Purpose

Document a safe path for bringing strength-training context from Heavy into this running site without turning the site into the source of truth for workout logging. Heavy remains the strength log; this site can surface concise planning and reflection context alongside running training.

## Possible Use Cases

- Review completed strength sessions beside each training week.
- Surface recent lower-body, upper-body/core, and calf/soleus work in weekly reflections.
- Compare strength consistency with running volume and key workouts.
- Link out to Heavy routines or completed sessions when a shareable URL is available.

## Safe API Handling

- Never commit API keys.
- Use `.env` or local environment variables.
- Add `.env` to `.gitignore`.
- Use `HEAVY_API_KEY` as the environment variable name.
- Do not expose the key in static site output.

Any future API work should run in a local script, private service, or secure build environment that reads `HEAVY_API_KEY` at runtime. It must not place the key in Hugo content, templates, JavaScript, generated HTML, or client-side requests.

## Phase 1: Read-Only Sync

Start with a local, read-only experiment that retrieves completed workouts and writes a private, reviewable summary. Validate the available fields, workout dates, exercise names, sets, reps, load, and any useful routine metadata before deciding whether anything belongs on the site.

## Phase 2: Strength Summary Cards

If the read-only data is reliable, generate small summary cards for a training week: completed lifting days, major movement patterns, and simple volume or consistency signals. Keep the full workout history in Heavy and show only context that helps interpret the running block.

## Phase 3: Possible Routine Generation

Consider routine generation only after read-only retrieval and summary cards are stable. Any generated routine should be reviewed before it reaches Heavy, respect the current running load, and avoid automatic changes to an active training plan.

## Open Questions

- Which completed-workout fields are available through the API, and how stable are they?
- Are webhooks available for completed workouts, edits, or deletions?
- Does the API support routine creation, or only retrieval and updates?
- What is the smallest strength summary that is useful beside a running week?
- Should any future sync remain local-only rather than run during site deployment?

<!-- TODO: Investigate Heavy API docs to determine whether routine creation is supported. Start with completed workout retrieval and webhooks only. -->
