---
name: setup
description: "Set up the current repository for StartUpWinner: a short interview, then project.yaml, a tagged TODO.md, and the competitor research for the Market tab. Shows the diff, never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Set up this repository (the current repository) for StartUpWinner, a dashboard that reads it from GitHub (read-only) and shows the project's stage, web / iOS / Android status, blocked and late items, and backlog.

Do not commit or push. When you are done, show me the diff and list every choice you weren't sure about, so I can review before I commit.

## 1. Read the repository

README, TODO.md, docs, package files, and deployment config (vercel.json, wrangler.toml, netlify.toml, app.json / eas.json, Xcode or Gradle projects, .env.example, Stripe or RevenueCat usage). Never read or copy real secrets (.env, .env.local, keys).

## 2. Interview me (one message, then wait)

Finish all your reading first, then write this message once. Some things only I know. Ask them all in ONE short message, numbered, and put what you found next to each so I can just confirm ("I found: …, right?"):

1. What the product does, the problem it solves and for whom (one sentence each).
2. What to track: (a) the web app, (b) the Android app, (c) the iOS app, (d) only the mobile apps (iOS and Android), or (e) all of them (web, iOS and Android). Other mixes are fine too, e.g. web and iOS. This sets `project.type` (a: web, b: android, c: ios, d: mobile, e: web+mobile, web and iOS: web+ios) and which checklist items apply; suggest the one the code points to.
3. Target launch date per platform, or "none yet".
4. Pricing: free, paid, how much (or "not decided").
5. Is it live anywhere already? The site's address, App Store or Play listing.
6. Which of these are done? A quick yes / no / doesn't apply per line: every methodology item marked [ask me] below that applies to my platforms.

Wait for my answers before writing anything. If I skip a question, leave that field out rather than guessing.

If no README or doc explains the product, also write `docs/idea.md` from my answers: the problem, who it's for, what it does, pricing, and the dates (a page, not an essay).

## 3. Write .startupwinner/project.yaml

```yaml
spec_version: 1
project:
  id: my-app                 # slug
  name: My App
  tagline: One line          # optional
  type: web+mobile           # web | ios | android | mobile (iOS + Android) | web+mobile | web+ios | web+android | api | extension | other
stage: mvp                   # idea | validate | mvp | prelaunch | ship | launch | grow | paused | killed
targets:                     # optional target dates per platform, YYYY-MM-DD
  web: 2026-12-01
  ios: 2026-12-15
  android: 2026-12-15
market:                      # optional, one sentence each
  problem: …
  target_user: …
  pricing: …
  differentiator: …          # one sentence: why people pick this over the competitors
deploy:                      # optional, only what exists
  web: { url: https://…, host: vercel }   # vercel | cloudflare | netlify | railway | fly | other
  ios: { bundle_id: …, app_store_id: "…" }
  android: { package: … }
services:                    # every paid or free dependency you can find
  - { name: supabase, category: database, plan: free, cost: { amount: 0, currency: USD, period: month }, billing: manual }
  # category: hosting | database | auth | email | ai | analytics | monitoring | domain | storage | payments | other
  # cost: null when unknown; period: month | year | one_time | usage
social:                      # optional
  - { platform: x, handle: … }
competitors:                 # step 6 fills these in
```

Rules: no secrets or keys anywhere in this file. Market, targets, type and deploy come from my answers and the repository. Stage is project-wide: set it to the first stage whose exit isn't met once TODO.md is tagged (idea: both items done; validate: a demand signal and the differentiator; mvp: the core flow working on a preview deploy; prelaunch: every item done or skipped; ship: every platform live; launch: launched on at least one channel; then grow). The dashboard checks the same rule.

## 4. Tag TODO.md

TODO.md stays the source of truth. Tag each checkbox that matches a methodology item below with an HTML comment at the end of its line (invisible when rendered):

```markdown
- [ ] **Play closed test:** 12 testers for 14 days <!-- sw:mobile.android.closed_testing -->
- [x] Privacy and terms pages live <!-- sw:prelaunch.legal -->
- [ ] Paid apps <!-- sw:mobile.iap skipped="apps are free in v1" -->
- [ ] Production access <!-- sw:mobile.android.production_access blocked="Google review" since=YYYY-MM-DD -->
```

- `[x]` done, `[ ]` to do, `[~]` in progress. One comment per tag; a line can carry several, and one item can be tagged on several lines (it is done only when all are checked).
- `skipped="reason"` for items that don't apply. `blocked="reason" since=YYYY-MM-DD` only for items waiting on someone else; never guess blocked.
- Don't reword, reorder or re-check existing lines; only append tags.
- Only tag items for the platforms in `project.type` (web items for web, iOS items for iOS, Android items for Android, shared mobile items for either).

## 5. Add what's missing

For every applicable item with no matching line:
- if the repository shows it is already done, add a checked line with the evidence (a file, a doc, a config) in a section "StartUpWinner methodology" under the done part of TODO.md;
- otherwise add an open line, in the section where it belongs: the text, then "(new, StartUpWinner, YYYY-MM-DD)", then the tag last.
- Items marked [dashboard checks] are ticked by the dashboard once the service is connected (uptime, Vercel deploys, Stripe, the App Store and Play through the GitHub Action). Tag them; tick one yourself only with clear evidence (a file, a config, or my answer). Never tick `validate.opportunity_score` and don't plan work for it: the dashboard computes it once 3+ competitors have pricing and features (step 6).
If there is no TODO.md, create one with sections for the current work, what's done, and later ideas, in the same style.

Never mark something done without evidence: a file, a config, or my answer in the interview. Items marked [ask me] are ticked only when I said yes ("done, per you, YYYY-MM-DD" as the evidence), skipped when I said they don't apply, and open otherwise.

## 6. Research the competition

So the dashboard's Market tab and opportunity score work from day one, research the competitors now (on the web; if you can't search the web, use the repo's own research docs and say so). Start from any the repository already names.
- Aim for the 5 to 8 that matter most: direct competitors first (same problem, same people), then the closest alternatives people use instead (including "a spreadsheet" or "doing nothing" when that's the real alternative).
- Use the web: their own sites and pricing pages, App Store and Google Play listings, Product Hunt, review sites, and the repo's own research docs if it has any.
- Prefer facts you can link to. If you can't verify something, leave the field out rather than guessing.

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

Also set `market.differentiator`: one sentence on why people pick this product over all of them. Keep every other part of project.yaml as it is. If I gave a differentiator in the interview, keep my words; otherwise propose one from what you found, and list it among the choices you weren't sure about.

Then, in TODO.md, check `validate.competitors_mapped` ([x], with "competitors in .startupwinner/project.yaml" as the evidence) once 3 or more competitors have pricing and features, and `validate.differentiator` only if I confirmed one. When you show me the diff, also list the sources you used.

## Methodology items

idea
- `idea.problem`: Problem and target user written in project.yaml
- `idea.manifest`: .startupwinner/ created and committed [dashboard checks]

validate
- `validate.competitors_mapped`: 3+ competitors listed with features and pricing
- `validate.differentiator`: One-sentence "why us instead of X" [ask me]
- `validate.demand_signal`: At least one real signal: waitlist sign-ups, 5 user conversations, pre-sales, search volume [ask me]
- `validate.pricing`: Pricing hypothesis written
- `validate.opportunity_score`: Opportunity score: the dashboard computes it once 3+ competitors have pricing and features [dashboard checks]

mvp
- `mvp.repo_from_template`: Started from the StartUpWinner template (or equivalent stack documented)
- `mvp.scope`: MVP scope frozen: ≤ 5 features listed in README
- `mvp.core_flow`: The one core flow works end to end [ask me]
- `mvp.auth`: Sign up / sign in / sign out
- `mvp.data`: Database with migrations in the repo
- `mvp.preview_deploy`: Preview deploy on every push [dashboard checks]

prelaunch
- `prelaunch.domain`: Custom domain with HTTPS [dashboard checks]
- `prelaunch.payments`: Live-mode payments + webhook handling (subscription created / failed / cancelled)
- `prelaunch.transactional_email`: Sign-up, password reset and receipt emails from your domain (SPF/DKIM set)
- `prelaunch.analytics`: Product analytics on key events
- `prelaunch.error_tracking`: Error tracking wired up (frontend + backend)
- `prelaunch.legal`: Privacy policy + terms pages live [dashboard checks]
- `prelaunch.account_deletion`: Users can delete their account (Apple requires this in-app if accounts exist)
- `prelaunch.landing`: Landing page: promise, pricing, call to action [dashboard checks]
- `prelaunch.backups`: Database backups on [ask me]

ship
- `web.production`: Production deploy on the custom domain (web only) [dashboard checks]
- `web.uptime`: Uptime monitor configured (web only) [dashboard checks]
- `web.first_payment`: First real payment received (web only) [dashboard checks]
- `mobile.app_config`: One codebase (Expo/EAS) with app.json/eas.json, icons, splash (iOS + Android only)
- `mobile.store_assets`: Screenshots per device size, description, keywords, support URL (iOS + Android only) [ask me]
- `mobile.iap`: In-app purchases for digital goods (stores require their billing; RevenueCat recommended) (iOS + Android only)
- `mobile.ios.dev_account`: Apple Developer Program ($99/yr) (iOS only) [ask me]
- `mobile.ios.app_record`: App record in App Store Connect, bundle ID registered (iOS only) [dashboard checks]
- `mobile.ios.privacy_labels`: App Privacy ("nutrition label") answers filled (iOS only) [ask me]
- `mobile.ios.testflight`: Build on TestFlight, tested by 3+ people (iOS only) [dashboard checks]
- `mobile.ios.review_submitted`: Submitted for App Review (iOS only) [dashboard checks]
- `mobile.ios.live`: Approved and live (iOS only) [dashboard checks]
- `mobile.android.dev_account`: Google Play Console ($25 one-time, identity verification) (Android only) [ask me]
- `mobile.android.internal_testing`: Build uploaded to the internal testing track (Android only) [dashboard checks]
- `mobile.android.data_safety`: Data safety form filled (Android only) [ask me]
- `mobile.android.closed_testing`: Closed test with 12+ testers for 14+ days (required for new personal accounts) (Android only) [dashboard checks]
- `mobile.android.production_access`: Production access granted (Android only) [dashboard checks]
- `mobile.android.live`: Live on Play Store (Android only) [dashboard checks]

launch
- `launch.channels`: 3 launch channels chosen (Product Hunt, Reddit, X, Hacker News, niche communities, newsletter) [ask me]
- `launch.assets`: Demo video/GIF, launch post copy [ask me]
- `launch.executed`: Launched on at least one channel [ask me]
- `launch.feedback_loop`: Feedback channel (email, Discord, in-app) monitored [ask me]
