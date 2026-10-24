---
name: focus
description: "Pick the one priority for this week with me, from the StartUpWinner dashboard's numbers and the repo, and record it as focus in .startupwinner/project.yaml. Never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Help me pick the one priority for this week (YYYY-Www (the ISO week of today)) for this project (the current repository), and record it in .startupwinner/project.yaml for the StartUpWinner dashboard.

Do not commit or push.

## The numbers this week
Ask me to paste them from the "This week's focus" box on the project's Overview in StartUpWinner. If I don't have them, work from the repository alone.

## 1. Look
Read .startupwinner/project.yaml (stage, targets, market, launch), TODO.md (open items, P1s, what's blocked) and the git log of the last 7 days (what actually moved).

## 2. Propose
Pick the ONE thing that would change the most this week, given the stage: before launch that's usually the item that unblocks the target date; after launch it's usually reliability, the first or next paying customers, or whatever made the numbers drop. Prefer fixing what's broken over starting something new. Tell me in a few lines: the priority, why it beats the alternatives (name the top 2 you didn't pick), and "done when", something I can check by Friday. Then wait for me to agree or pick another.

## 3. Record
Once I agree, set this in .startupwinner/project.yaml (replace any older `focus:`, keep everything else):

```yaml
focus:
  week: YYYY-Www (the ISO week of today)
  priority: one short sentence
  why: one sentence
  done_when: something checkable by the end of the week
```

Write only inside `.startupwinner/`: never edit TODO.md or other project files. Show me the diff. Today is YYYY-MM-DD.
