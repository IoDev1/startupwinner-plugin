---
name: launch
description: "Prepare the launch: pick channels, then write ready-to-paste copy for Product Hunt, Show HN, Reddit, X and more into launch/, and set the launch date and channels in .startupwinner/project.yaml. Never posts, never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Prepare the launch of this project (the current repository) and write the launch kit into the repo, for the StartUpWinner dashboard's Launch tab.

Do not commit or push, and don't post anything anywhere. When you are done, show me the diff and list the choices you weren't sure about.

## 1. Read
README, docs, the landing page copy, .startupwinner/project.yaml (project, market, competitors, launch) and TODO.md, so you know what the product does, for whom, at what price, and how it differs from the competitors.

## 2. Choose
If `launch.channels` in project.yaml is empty, propose the 3 to 5 channels where the target user actually is, from: `product_hunt`, `show_hn`, `reddit`, `x`, `linkedin`, `indie_hackers`, `directories`, `newsletter`, `app_stores` (mobile apps only). Explain each choice in one line and ask me before writing them. Also ask me for the launch date if `launch.date` is missing (never guess it).

## 3. Write the kit
Create `launch/` at the repo root with one Markdown file per chosen channel (`launch/product-hunt.md`, `launch/show-hn.md`, …) plus `launch/week.md` for the posts after launch day (day 1 thank-you, day 3 lessons, day 7 recap). In each file:
- the copy, ready to paste, in the channel's own voice and within its limits (Product Hunt tagline 60 characters, Show HN title 80, App Store subtitle 30, Play short description 80, X posts 280);
- the channel's checklist (images, video, accounts) with what's already in the repo ticked;
- for Reddit, the specific subreddits where the target user is, with each one's self-promotion rule.
Write like a person, not an ad: concrete, no hype words, no invented numbers or quotes. Leave [brackets] where only I know the answer.

## 4. Update project.yaml and TODO.md
- Set `launch.date` (from me) and `launch.channels` (the ids above). Keep every other part of project.yaml.
- In TODO.md, if they aren't there yet, add open lines for the launch items, tagged `<!-- sw:launch.channels -->`, `<!-- sw:launch.assets -->`, `<!-- sw:launch.executed -->`, `<!-- sw:launch.feedback_loop -->`. Check `launch.channels` once 3 are chosen; leave the others to me.

After launching, I add each live post to `launch.posted` (`- { channel: product_hunt, url: https://…, date: YYYY-MM-DD }`) and the dashboard ticks launch.executed. Today is YYYY-MM-DD.
