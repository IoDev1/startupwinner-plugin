---
name: setup
description: "Set up the current repository for StartUpWinner: a short interview, then the project file, the checklist, the project rules and the competitor research, all in .startupwinner/ (plus one line in CLAUDE.md). Shows the diff, never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Set up this repository (the current repository) for StartUpWinner, a dashboard that reads it from GitHub (read-only) and shows the project's stage, web / iOS / Android status, blocked and late items, and backlog.

Do not commit or push. When you are done, show me the diff and list every choice you weren't sure about, so I can review before I commit. On a re-run, also list what changed since the last setup.

**Where you write:** only inside `.startupwinner/`, plus one line in the root `CLAUDE.md` (step 7). Read anything in the repository, but never edit the project's own files: not TODO.md, not the README, not the code. If you need to change one of them, put a copy in `.startupwinner/` and change the copy.

## 1. Read the repository

README, TODO.md, docs, package files, and deployment config (vercel.json, wrangler.toml, netlify.toml, app.json / eas.json, Xcode or Gradle projects, .env.example, Stripe or RevenueCat usage). Never read or copy real secrets (.env, .env.local, keys).

**Is this a re-run?** If .startupwinner/project.yaml already exists, the project was set up before and this run refreshes it: start from that file and .startupwinner/checklist.md (or, for older setups, the tags in TODO.md), keep every answer I gave last time, and look for what changed since (new files, services, platforms, store records, items now done). Re-check every methodology item; tick the ones that now have evidence, and never un-tick or remove anything without listing it for me.

## 2. Interview me (one message, then wait)

Finish all your reading first, then write this message once. On a re-run, ask only what's missing in project.yaml or what the repository suggests has changed ("you now have an eas.json: still iOS only?"), and skip the interview when nothing is. Some things only I know. Ask them all in ONE short message, numbered, and put what you found next to each so I can just confirm ("I found: …, right?"):

1. What the product does, the problem it solves and for whom (one sentence each).
2. What to track: (a) the web app, (b) the Android app, (c) the iOS app, (d) only the mobile apps (iOS and Android), or (e) all of them (web, iOS and Android). Other mixes are fine too, e.g. web and iOS. This sets `project.type` (a: web, b: android, c: ios, d: mobile, e: web+mobile, web and iOS: web+ios) and which checklist items apply; suggest the one the code points to.
3. Target launch date per platform, or "none yet".
4. Pricing: free, paid, how much (or "not decided").
5. Is it live anywhere already? The site's address, App Store or Play listing.
6. Which of these are done? A quick yes / no / doesn't apply per line: every methodology item marked [ask me] below that applies to my platforms.

Wait for my answers before writing anything. If I skip a question, leave that field out rather than guessing.

If no README or doc explains the product, also write `.startupwinner/idea.md` from my answers: the problem, who it's for, what it does, pricing, and the dates (a page, not an essay).

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

Rules: no secrets or keys anywhere in this file. Market, targets, type and deploy come from my answers and the repository. Stage is project-wide: set it to the first stage whose exit isn't met once the checklist is written (idea: both items done; validate: a demand signal and the differentiator; mvp: the core flow working on a preview deploy; prelaunch: every item done or skipped; ship: every platform live; launch: launched on at least one channel; then grow). The dashboard checks the same rule.

## 4. Write .startupwinner/checklist.md

The methodology checklist lives in this file, in our folder, and I tick it there. TODO.md stays mine: read it for evidence, never edit it. Write every methodology item below that applies to my platforms, grouped under a heading per stage, one checkbox each with its tag in an HTML comment at the end of the line (invisible when rendered):

```markdown
# Checklist

## Ship
- [ ] **Play closed test:** 12 testers for 14 days <!-- sw:mobile.android.closed_testing -->
- [x] **Privacy and terms pages live:** app/privacy and app/terms <!-- sw:prelaunch.legal -->
- [ ] **Paid apps** <!-- sw:mobile.iap skipped="apps are free in v1" -->
- [ ] **Production access** <!-- sw:mobile.android.production_access blocked="Google review" since=YYYY-MM-DD -->
```

- `[x]` done, `[ ]` to do, `[~]` in progress. Each done line names its evidence after the title: a file, a config, a TODO.md line ("TODO.md: Privacy page"), or my answer.
- `skipped="reason"` for items that don't apply. `blocked="reason" since=YYYY-MM-DD` only for items waiting on someone else; never guess blocked.
- Only items for the platforms in `project.type` (web items for web, iOS items for iOS, Android items for Android, shared mobile items for either).
- Items marked [dashboard checks] are ticked by the dashboard once the service is connected (uptime, Vercel deploys, Stripe, the App Store and Play through the GitHub Action). List them; tick one yourself only with clear evidence (a file, a config, or my answer). Never tick `validate.opportunity_score` and don't plan work for it: the dashboard computes it once 3+ competitors have pricing and features (step 6).

## 5. On a re-run, move old tags out of TODO.md

Projects set up before this file existed have `<!-- sw:… -->` tags in TODO.md. If you find any: carry each item's state (and any skipped/blocked) into checklist.md, then remove only those tag comments from TODO.md, so its lines read exactly as I wrote them. That is the one change you may make to TODO.md, and only to undo what StartUpWinner added; list it for me. An existing checklist.md: update it, keeping my ticks.

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
    revenue_model: subscription            # how they make money: subscription, one-time, ads, sponsors, donations, paid hosting, marketplace fees, none
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

Also set `market.differentiator`: one sentence on why people pick this product over all of them. Keep every other part of project.yaml as it is. Put any text that contains `: ` or ` #` in quotes, so the file stays valid YAML (an invalid file stops the dashboard from syncing). If I gave a differentiator in the interview, keep my words; otherwise propose one from what you found, and list it among the choices you weren't sure about.

Then, in .startupwinner/checklist.md, check `validate.competitors_mapped` ([x], with "competitors in .startupwinner/project.yaml" as the evidence) once 3 or more competitors have pricing and features, and `validate.differentiator` only if I confirmed one. When you show me the diff, also list the sources you used.

## 7. Project rules for your agent

Write `.startupwinner/CLAUDE.md`, short, for any agent working in this repository:
- what the product is, for whom, and the stage (one paragraph, from project.yaml and idea.md);
- the stack and where things are (from what you read);
- "The StartUpWinner checklist is .startupwinner/checklist.md: when you finish something on it, tick it there with the evidence. Never edit TODO.md's lines for StartUpWinner.";
- anything the repository already asks of agents (an existing CLAUDE.md, AGENTS.md or contributing guide): point to it, don't copy it.

Then make sure the root `CLAUDE.md` loads it: if the line `@.startupwinner/CLAUDE.md` isn't there, add exactly that one line at the end (create the file with just that line if there is none). Change nothing else in it.

## 8. Offer the dashboard connection (last, after the diff)

The dashboard can answer you directly over MCP (read-only): what's late, what's next, the numbers. If you are Claude Code, check with `claude mcp list` whether `startupwinner` is already connected; if it is, say so and skip this step. Otherwise end your message with these steps for me, as they are:

1. Commit and push, so the dashboard reads the new files.
2. Open https://start-up-winner.vercel.app/settings/agents, create a token, and run the `claude mcp add` command it shows in a terminal (once per computer, not per project).
3. Restart Claude Code; from then on you can ask me "what should I do today?" in any project.

Never ask me to paste the token into this chat: the command keeps it in Claude Code's settings.

## Methodology items

idea
- `idea.problem`: Problem and target user written in project.yaml
- `idea.manifest`: .startupwinner/ created and committed [dashboard checks]

validate
- `validate.competitors_mapped`: 3+ competitors listed with features and pricing
- `validate.differentiator`: One-sentence "why us instead of X" [ask me]
- `validate.demand_signal`: At least one real signal: waitlist sign-ups, 5 user conversations, pre-sales, search volume [ask me]
- `validate.pricing`: Pricing hypothesis written
- `validate.opportunity_score`: Opportunity score final: the dashboard shows it from day one, provisional until 3+ competitors have pricing and features [dashboard checks]

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
- `prelaunch.security_check`: Security check passed: /startupwinner:security with no critical or high findings left open
- `prelaunch.qa_pass`: Tested like a real user: /startupwinner:qa flows pass on a preview deploy (sign-up, data isolation, payments in test mode, errors, mobile)

ship
- `web.production`: Production deploy on the custom domain (web only) [dashboard checks]
- `web.uptime`: Uptime monitor configured (web only) [dashboard checks]
- `web.first_payment`: First real payment received (web only) [dashboard checks]
- `mobile.app_config`: App project ready for the stores: Expo/EAS (app.json/eas.json), or a native Xcode / Gradle / Flutter project; real bundle id, icons and splash (iOS + Android only)
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
