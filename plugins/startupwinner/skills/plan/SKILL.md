---
name: plan
description: "Plan the build before coding: interview, a spec with checks per step, the data model and access rules, a design file for the look, verification and analytics, in .startupwinner/. Expert-backed, never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Run the StartUpWinner **plan** playbook on this project (the current repository), before building a product or a larger feature. Today is YYYY-MM-DD.

Plan the build so your agent works from a clear, checkable plan instead of guessing. The checks below come from expert practice (Anthropic's Claude Code guidance, OWASP, web.dev, and builders who shipped), in priority order.

Do not commit or push: when you're done, show me the diff and the summary.

## Before you start
- Read `.startupwinner/project.yaml`, `.startupwinner/checklist.md`, `.startupwinner/CLAUDE.md` and the README to learn the product, the platforms and how to run it. TODO.md is mine: read it, never edit it.
- Skip checks that don't apply (no payments yet, no database, no web app) and say why in one line.
- At most 8 fixes this run, unless I said otherwise: each one costs time and tokens, and I review between runs.

## Rules
- Interview me first, in ONE message with all your questions, then wait. Draft answers from the repository where you can, so I only confirm.
- Write the plan in `.startupwinner/spec.md` (create or update it), the checks in `.startupwinner/checklist.md`, and, for an app with a real interface, `.startupwinner/design.md`. Don't create PRD/ARCHITECTURE/RULES/TASKS/PROGRESS files: the spec, the checklist, the design file and a short `.startupwinner/CLAUDE.md` cover them.
- Don't write product code in this run: the plan is the deliverable.

## The checks
1. **The problem, the buyer and the one core job, in 3 to 5 lines (in project.yaml's `market` and at the top of the spec).** Why: the whole product is scoped to one job, and every later decision is judged against it. *Needs you:* confirm the wording.
2. **A spec for the build: the files and interfaces involved, what's out of scope, and how to check it works end to end.** Why: a spec written after an interview is the most reliable way to brief an agent on larger work.
3. **The validation signal and a kill date: what proves demand (a pre-order, a deposit, a waitlist with replies) and by when you'll decide.** Why: even experienced builders see most ideas fail; a time box stops sunk cost. *Needs you:* choose the signal and the date.
4. **A boring, known stack: reuse the existing stack or a starter, and flag any new framework that has no clear reason.** Why: agents are most reliable on mainstream stacks, and boring ships faster.
5. **Every feature broken into small steps, each with a pass/fail check, in the checklist.** Why: a check per step stops the agent from calling things done too early.
6. **Payments in the first version, in the provider's test mode.** Why: people paying is the validation that counts. *Needs you:* create the payment account and test keys.
7. **A data model where every user-owned row has an owner (user_id or org_id), with access rules (for Supabase, RLS policies) planned before any table.** Why: broken access control is the main way AI-built apps leak data.
8. **For an app with a real interface, a short `.startupwinner/design.md`: colours, fonts, spacing and radius as tokens, the core components and their states (button, input, card, empty, loading, error), light and dark, and 3 to 5 rules (for example "one primary button per screen"); taken from the existing styles when there are any, written as tokens and rules, not prose.** Why: without it the agent invents a new look on every screen. *Needs you:* confirm the look, or point to a site you like.
9. **A short `.startupwinner/CLAUDE.md`: run, test and build commands, rules that differ from the defaults, key decisions, gotchas; nothing the code already says.** Why: a long rules file gets ignored.
10. **One command to start the app and one to run the tests, written in the spec.** Why: every session should start by running the app and the tests.
11. **Verification set up: tests run, typecheck, lint and build pass, and one end-to-end check of the core job is planned.** Why: giving the agent a way to check its own work is the biggest quality lever.
12. **Rules that must always hold (format after edits, never touch .env or applied migrations) proposed as Claude Code hooks.** Why: hooks always run; written rules are only advice. *Needs you:* approve any change to the project's settings.
13. **1 or 2 launch channels and the analytics events (sign-up, the core job done, payment).** Why: few channels done well beat many, and you can't improve what you don't measure. *Needs you:* pick the channels.
14. **Work one checklist step at a time and commit after each, noting progress in the checklist.** Why: sessions forget; git history and the checklist don't.

## When something needs me
For every check that needs a person, write `.startupwinner/guides/plan-<number>.md` with: what and why (two lines), numbered steps with exact links and clicks, which key with the smallest access and where it goes (never this chat, never the code), how to see it worked, and what you'll do next. Then carry on with the other checks.

## When you're done
Write `.startupwinner/plan.md`: today's date, then one line per check: ✅ passed (with the evidence), 🔧 fixed (what changed), ⚠️ needs you (the guide), or — skipped (why). If a methodology item in `.startupwinner/checklist.md` is now proven (for example `prelaunch.error_tracking` or `prelaunch.legal`), tick it with the evidence. Then show me the summary, the guides waiting for me, and the diff.

## Never
- Never ask me to paste a password, key or token into this chat, never write one into a file, never print an environment variable's value.
- Never create accounts, accept terms, pay, or post anything in my name.
- Never delete data, apply migrations to a live database, rewrite git history, or push.
- Never edit TODO.md.
