---
name: new
description: "Start a new product from the StartUpWinner starter (Next.js, Supabase, Stripe, Expo): create the repo from the template and fill in its name, pitch and dates. Never pushes."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Start a new product from the StartUpWinner starter (IoDev1/startupwinner-starter): Next.js on Vercel, Supabase, Stripe, Resend, PostHog, Sentry and an Expo app, with the StartUpWinner checklist already in .startupwinner/checklist.md, ready for the StartUpWinner dashboard.

## 1. Ask me first
Ask, in one message: the product name, one sentence on the problem and who has it, what to build and track ((a) the web app, (b) the Android app, (c) the iOS app, (d) only the mobile apps, or (e) all of them), the price idea, and target launch dates per platform (or "none yet"). Wait for my answers.

## 2. Create the repo
Pick a repo name from the product name (lowercase, dashes). If the GitHub CLI is installed and signed in (`gh auth status`), run:

    gh repo create <repo-name> --private --template IoDev1/startupwinner-starter --clone

then work inside the new folder. Otherwise tell me to open https://github.com/IoDev1/startupwinner-starter/generate, create a private repo, and clone it; continue once I say it's cloned.

## 3. Make it theirs
- `apps/web/src/lib/site.ts`: name, promise (one sentence from my answer), description, prices. Leave the feature placeholders for me.
- `apps/mobile/app.json`: name, slug, scheme, ios.bundleIdentifier and android.package (com.<repo-name without dashes>.app unless I gave one). If I only want web, delete apps/mobile and mark the mobile items in .startupwinner/checklist.md skipped="web only"; if I want only mobile, mark the web items skipped="mobile only" (keep apps/web: it serves account deletion and payments); if only one store, mark the other store items skipped. Never remove tagged lines.
- `package.json` name, the README title and first line.
- `.startupwinner/project.yaml`: project id, name, tagline, type (web, ios, android, mobile, web+mobile, web+ios or web+android), targets (only the dates I gave), market.problem, market.target_user, market.pricing, the bundle id and package. Keep every other part.
- `.startupwinner/checklist.md`: tick `idea.problem` now that it's written. Don't touch the other tags. TODO.md is mine for my own todos: title it "<name> ToDo" and leave the rest.

## 4. Check and hand back
Run `pnpm install` and `pnpm build`. Do not push. Show me the diff, then commit locally with the message "Start <name> from the StartUpWinner starter" once I agree. Today is YYYY-MM-DD.

Finally tell me the next steps: push, add the repo to the StartUpWinner GitHub App so the dashboard sees it, then follow README "Set up the services" in order.
