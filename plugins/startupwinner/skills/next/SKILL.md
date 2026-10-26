---
name: next
description: "Work through the StartUpWinner checklist on its own: do every item it can in the repo (up to 5 a run), and stop only for what needs a person, with a step-by-step guide for each in .startupwinner/guides/. Shows the diff, never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Work through the StartUpWinner checklist of this project (the current repository) on your own: do every item you can in the repository, and stop only for what needs me. Today is YYYY-MM-DD.

Do not commit or push: when you stop, show me the diff and a short summary.

## 1. Find the work

- Read `.startupwinner/project.yaml` (platforms, stage, dates), `.startupwinner/checklist.md` (the items: `[ ]` to do, `[~]` in progress, `[x]` done), `.startupwinner/CLAUDE.md` and TODO.md (my own list: read it, never edit it).
- If the `startupwinner` MCP tools are connected, call `get_project_status` for this repo: it says what's late, blocked and next, from the live dashboard.
- No `.startupwinner/checklist.md`? Stop and tell me to run `/startupwinner:setup` first.
- Work in this order: late items first, then the current stage's open items from top to bottom, then the next stage's. Skip items marked `blocked=` or `skipped=`, and `validate.opportunity_score` (the dashboard computes it).
- At most 5 items this run, unless I said otherwise when I started you: each item costs time and tokens, and I review between runs.

## 2. For each item, decide who does it

**You do it** when it's work in the repository: code, configuration, tests, docs, copy, pages (privacy, terms, landing), wiring a service whose key will come from an environment variable, adding a variable's name to `.env.example`.
- Do the smallest change that meets the item, the way the repository already does things.
- Check it: run the build, the tests and the linter if the project has them; for a page, run it and look.
- Tick it in `.startupwinner/checklist.md`: `[x]` with the evidence after the title (the file or the check that proves it). Half done: `[~]` with what's left.

**A playbook does it** for `prelaunch.security_check` and `prelaunch.qa_pass`: each is a whole run of its own (`/startupwinner:security`, `/startupwinner:qa`). Don't do them inside this run; list them at the end as the next command to run, security first.

**I do it** when it needs a person: creating an account, accepting terms, paying, getting or pasting an API key, anything in a store console (App Store Connect, Google Play), DNS and domains, legal choices, talking to users, and every decision about the product (pricing, the differentiator, launch channels).
- Don't try to do these yourself and don't stop at the first one: write the guide (step 3), then carry on with the items you can do.

## 3. A guide for every stop

For each item that needs me, write `.startupwinner/guides/<item id>.md` (create the folder if needed):

1. **What and why**, in two lines, in plain words.
2. **Steps**, numbered, each one a single action: the exact page (a link), what to click, what to fill in. Assume I've never done it before.
3. **Keys and permissions:** which key or token, with the smallest access that works (read-only, restricted, one project), and where it goes: the hosting provider's environment variables or the repository's secrets, never in the code, never in this chat. Name the variable exactly as the code expects it.
4. **Done when:** how I can see it worked (a page, a green check, a test email).
5. **What you'll do next** once I say it's done.

Decisions get a guide too, with 2 or 3 options and what each one means for the project; recommend one.

## 4. When you stop

Stop when you've done 5 items, or when every open item needs me. Then show me:
- what you did, item by item, with how you checked it;
- the guides waiting for me, most urgent first, each with its file and the one-line "what and why";
- the diff, for me to review and commit.

When I come back and say a guide is done, check what you can (the variable is used, the page answers, the build passes), tick the item with "done, per you, YYYY-MM-DD" when only I can see it, and continue from step 1.

## Never

- Never ask me to paste a password, key or token into this chat, never write one into a file, and never print the value of an environment variable.
- Never create accounts, accept terms, buy anything, or post anything in my name.
- Never delete data, rewrite git history, or push.
- Write only in the repository and `.startupwinner/`; never edit TODO.md.
