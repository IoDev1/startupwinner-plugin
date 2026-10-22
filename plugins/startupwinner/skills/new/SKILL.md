---
name: new
description: "Start a new product from the StartUpWinner starter (Next.js, Supabase, Stripe, Expo): create the repo from the template and fill in its name, pitch and dates. Never pushes."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Start a new product from the StartUpWinner starter (IoDev1/startupwinner-starter): Next.js on Vercel, Supabase, Stripe, Resend, PostHog, Sentry and an Expo app, with a TODO.md already tagged for the StartUpWinner dashboard.

## 1. Ask me first
Ask, in one message: the product name, one sentence on the problem and who has it, web and/or mobile, the price idea, and target launch dates per platform (or "none yet"). Wait for my answers.

## 2. Create the repo
Pick a repo name from the product name (lowercase, dashes). If the GitHub CLI is installed and signed in (`gh auth status`), run:

    gh repo create <repo-name> --private --template IoDev1/startupwinner-starter --clone

then work inside the new folder. Otherwise tell me to open https://github.com/IoDev1/startupwinner-starter/generate, create a private repo, and clone it; continue once I say it's cloned.

## 3. Make it theirs
- `apps/web/src/lib/site.ts`: name, promise (one sentence from my answer), description, prices. Leave the feature placeholders for me.
- `apps/mobile/app.json`: name, slug, scheme, ios.bundleIdentifier and android.package (com.<repo-name without dashes>.app unless I gave one). If I only want web, delete apps/mobile and mark the mobile items in TODO.md skipped="web only" instead of removing them.
- `package.json` name, the README title and first line.
- `.startupwinner/project.yaml`: project id, name, tagline, type (web, mobile or web+mobile), targets (only the dates I gave), market.problem, market.target_user, market.pricing, the bundle id and package. Keep every other part.
- TODO.md: title "<name> ToDo"; tick `idea.problem` now that it's written. Don't touch the other tags.

## 4. Check and hand back
Run `pnpm install` and `pnpm build`. Do not push. Show me the diff, then commit locally with the message "Start <name> from the StartUpWinner starter" once I agree. Today is YYYY-MM-DD.

Finally tell me the next steps: push, add the repo to the StartUpWinner GitHub App so the dashboard sees it, then follow README "Set up the services" in order.
