---
name: speed
description: "Measure first, then fix what users feel (slow queries, the largest image, third-party scripts, JavaScript size, layout shift) and measure again. Report in .startupwinner/speed.md, never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Run the StartUpWinner **speed** playbook on this project (the current repository), once it works, before and after launch. Today is YYYY-MM-DD.

Make the app feel fast where users notice, measured before and after. The checks below come from expert practice (Anthropic's Claude Code guidance, OWASP, web.dev, and builders who shipped), in priority order.

Do not commit or push: when you're done, show me the diff and the summary.

## Before you start
- Read `.startupwinner/project.yaml`, `.startupwinner/checklist.md`, `.startupwinner/CLAUDE.md` and the README to learn the product, the platforms and how to run it. TODO.md is mine: read it, never edit it.
- Skip checks that don't apply (no payments yet, no database, no web app) and say why in one line.
- At most 8 fixes this run, unless I said otherwise: each one costs time and tokens, and I review between runs.

## Rules
- Measure first and last, the same way, and write both in `.startupwinner/speed.md`. A change without a before/after number doesn't count.
- Measure a production build (`next build && next start` or the preview deploy), never the dev server.
- One change at a time; keep each one that measurably helps, revert the rest.
- The targets are Google's Core Web Vitals at the 75th percentile, mobile and desktop: LCP 2.5 s or less, INP 200 ms or less, CLS 0.1 or less.

## The checks
1. **Measure from real users first: LCP, INP and CLS on mobile and desktop (Vercel Speed Insights, PageSpeed Insights, or web-vitals reporting), then pick the 1 to 3 slowest key pages.** Why: fix what users feel, with a baseline to prove it. *Needs you:* turn on the hosting provider's speed dashboard.
2. **Find slow database queries: EXPLAIN them, add indexes on the columns used to filter, join and sort, including the columns access rules filter on (and use `(select auth.uid())` in Supabase policies).** Why: often the biggest win for dashboards and lists.
3. **Remove N+1 queries and waterfalls: fetch in parallel, batch or join, and don't call your own API routes from server components.** Why: round-trips add up.
4. **Fix the largest element on screen (the LCP): the hero image through the framework's image component with high priority, NOT lazy-loaded, with sizes and dimensions; fonts through the framework's font loader.** Why: the LCP is usually one image or one block of text.
5. **Load third-party scripts late: chat widgets and embeds after the page is usable, analytics after it's interactive; delete unused tags.** Why: third-party code competes with your own.
6. **Ship less JavaScript: keep client-only code small, run the bundle analyzer, load heavy client-only parts on demand.** Why: less JavaScript means faster loads and quicker responses to taps.
7. **Make pages static or cached where you can: no per-request data in the root layout, dynamic parts wrapped in Suspense.** Why: pages served from the CDN start faster.
8. **Stream the slow parts with loading states and skeletons the same size as the final content.** Why: it feels faster without content jumping around.
9. **Reserve space for everything that loads late (images, embeds, banners) and animate with transforms only.** Why: keeps layout shift (CLS) under 0.1.
10. **Paginate or virtualize lists that can grow, and select only the columns you show.** Why: keeps pages and payloads small.
11. **Move slow work off the request: emails, webhook fan-out, AI calls, image processing go to background jobs.** Why: users should only wait for what they need. *Needs you:* a queue service account, if one is needed.
12. **Every image through the framework's image component (WebP is often the default; AVIF is optional), lazy below the fold.** Why: smaller images with no extra work.
13. **Back and forward navigation can use the browser cache: no unload listeners, no `no-store` on pages without a reason.** Why: instant back and forward.
14. **Only if INP is over 200 ms: profile, split long tasks, memoize the hot components.** Why: re-render work pays off only where it's measured.
15. **Measure again with the same tools and write the before/after numbers per page.** Why: evidence, so nobody undoes the gain.

## When something needs me
For every check that needs a person, write `.startupwinner/guides/speed-<number>.md` with: what and why (two lines), numbered steps with exact links and clicks, which key with the smallest access and where it goes (never this chat, never the code), how to see it worked, and what you'll do next. Then carry on with the other checks.

## When you're done
Write `.startupwinner/speed.md`: today's date, then one line per check: ✅ passed (with the evidence), 🔧 fixed (what changed), ⚠️ needs you (the guide), or — skipped (why). If a methodology item in `.startupwinner/checklist.md` is now proven (for example `prelaunch.error_tracking` or `prelaunch.legal`), tick it with the evidence. Then show me the summary, the guides waiting for me, and the diff.

## Never
- Never ask me to paste a password, key or token into this chat, never write one into a file, never print an environment variable's value.
- Never create accounts, accept terms, pay, or post anything in my name.
- Never delete data, apply migrations to a live database, rewrite git history, or push.
- Never edit TODO.md.
