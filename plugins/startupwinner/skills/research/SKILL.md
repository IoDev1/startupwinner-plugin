---
name: research
description: "Research the project's competitors on the web and record pricing, features, strengths, weaknesses and our edge in .startupwinner/project.yaml. Shows the diff and sources, never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Research the competition for this project (the current repository) and record it in .startupwinner/project.yaml, for the StartUpWinner dashboard's Market tab.

Do not commit or push. When you are done, show me the diff and the sources you used.

## 1. Understand the product
Read the README, docs and .startupwinner/project.yaml (market.problem, market.target_user, market.pricing) to know what the product does, for whom, and at what price.

## 2. Find the competitors
If .startupwinner/project.yaml already lists competitors, start from them, check each one again, and add the ones that are missing; otherwise find them.
- Aim for the 5 to 8 that matter most: direct competitors first (same problem, same people), then the closest alternatives people use instead (including "a spreadsheet" or "doing nothing" when that's the real alternative).
- Use the web: their own sites and pricing pages, App Store and Google Play listings, Product Hunt, review sites, and the repo's own research docs if it has any.
- Prefer facts you can link to. If you can't verify something, leave the field out rather than guessing.

## 3. Write them into project.yaml
Replace the `competitors:` list with entries in this format (everything but name is optional):

```yaml
competitors:
  - name: Example
    url: https://example.com
    pricing: "Free; Pro $8/mo"             # their actual public prices
    audience: who it's for, in a few words
    features: [feature one, feature two]   # the 3 to 6 that matter for this comparison
    strengths: what they do better than us
    weaknesses: where they fall short for our target user
    our_edge: why our target user would pick us instead
    ios_id: "1234567890"                   # App Store id, if they have an app
    android_package: com.example.app       # if they have an Android app
    notes: anything else worth knowing (size, funding, recent changes)
    checked_at: YYYY-MM-DD
```

Also set `market.differentiator`: one sentence on why people pick this product over all of them. Keep every other part of project.yaml as it is.

## 4. Tick the checklist
In `.startupwinner/checklist.md`, check `validate.competitors_mapped` ([x], "competitors in .startupwinner/project.yaml" as the evidence) once 3 or more competitors have pricing and features. Write only inside `.startupwinner/`: never edit TODO.md or other project files. (No checklist.md yet? Say so: `/startupwinner:setup` creates it.)
