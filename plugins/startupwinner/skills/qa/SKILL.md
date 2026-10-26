---
name: qa
description: "Click through the product like a real user before launch (sign-up, data isolation, payments in test mode, errors, mobile) and fix what breaks with a test first. Report in .startupwinner/qa.md, never commits."
disable-model-invocation: true
---

Wherever these instructions say YYYY-MM-DD, use today's date. "The current repository" is the repo you are in (its GitHub name is in `git remote get-url origin`).

Run the StartUpWinner **qa** playbook on this project (the current repository), before launch, and after big changes. Today is YYYY-MM-DD.

Click through the product like a real user before launch, and fix what breaks. The checks below come from expert practice (Anthropic's Claude Code guidance, OWASP, web.dev, and builders who shipped), in priority order.

Do not commit or push: when you're done, show me the diff and the summary.

## Before you start
- Read `.startupwinner/project.yaml`, `.startupwinner/checklist.md`, `.startupwinner/CLAUDE.md` and the README to learn the product, the platforms and how to run it. TODO.md is mine: read it, never edit it.
- Skip checks that don't apply (no payments yet, no database, no web app) and say why in one line.
- At most 8 fixes this run, unless I said otherwise: each one costs time and tokens, and I review between runs.

## Rules
- Test on the local dev server or a preview deploy, with test accounts and the payment provider's test mode. Never use production data or real cards, and never sign in as a real user.
- Drive a real browser: Playwright (MCP or CLI) or Claude in Chrome if you have them; otherwise run the app and use what you can (curl, the test runner), and list the flows a person must click through. For iOS and Android apps, use the simulator or emulator if available.
- A protected preview needs a bypass token: never ask me to paste it here. If you need one, write a guide for putting it in an environment variable.
- For every failure: write a failing test first, then fix it, then re-run everything. Don't batch many fixes into one pass.
- Record evidence for each flow (the command output, a screenshot or a short description of what you saw) in `.startupwinner/qa.md`.

## The checks
1. **First run the tests: build, typecheck and lint pass.** Why: it's the baseline, and it shows how the project runs.
2. **Sign up, verify the email, log out, log in again: the data is still there.** Why: it's the first thing every user does, and the most common break. *Needs you:* access to a test inbox, if verification emails are real.
3. **Sign-in errors: wrong password, empty form, email already taken, password reset end to end, an expired or reused reset link.** Why: error paths are where generated code is weakest.
4. **Users can't see each other's data: as user B, try to view, edit or delete user A's records, in the UI and by calling the API or database directly with B's session and with the public key.** Why: the most damaging bug in AI-built apps.
5. **Payments in test mode: success, decline, cancel, refund; the webhook arrives and is verified; access is granted and removed; reloading during checkout is safe.** Why: money flows break quietly. *Needs you:* the payment provider's test keys.
6. **The core job end to end as a brand-new user, with evidence.** Why: agents skip end-to-end testing unless told to.
7. **Every form with bad input: blank, very long, the wrong format, and script tags.** Why: it catches missing validation and cross-site scripting.
8. **Empty states on every list and dashboard, and the first-run experience.** Why: a new user always sees the empty version first.
9. **Error states: a 404 page, a 500 page, an API failure, a slow network.** Why: unhandled errors are now on OWASP's top 10.
10. **A phone-sized screen: navigation, forms and checkout.** Why: many first visits come from phones through social links.
11. **If `.startupwinner/design.md` exists, the key pages follow it: its colours, fonts and components, in light and dark, on desktop and phone.** Why: inconsistent screens look unfinished and cost trust.
12. **Navigation: every link, the back button after an action, reloading, opening a deep link while logged out (to the login, then back).** Why: state often breaks after navigating.
13. **Email links: verification, password reset, unsubscribe (one click, works logged out).** Why: a common break, and unsubscribe is required by law for marketing email.
14. **No errors in the browser console or failed network requests on the key pages.** Why: a cheap signal of hidden failures.
15. **Whatever changed recently, and the flows next to it.** Why: regressions hide next to the change.
16. **A fresh review: a separate subagent checks the diff and the QA evidence against the spec or checklist.** Why: whoever wrote the code shouldn't grade it.

## When something needs me
For every check that needs a person, write `.startupwinner/guides/qa-<number>.md` with: what and why (two lines), numbered steps with exact links and clicks, which key with the smallest access and where it goes (never this chat, never the code), how to see it worked, and what you'll do next. Then carry on with the other checks.

## When you're done
Write `.startupwinner/qa.md`: today's date, then one line per check: ✅ passed (with the evidence), 🔧 fixed (what changed), ⚠️ needs you (the guide), or — skipped (why). If a methodology item in `.startupwinner/checklist.md` is now proven (for example `prelaunch.error_tracking` or `prelaunch.legal`), tick it with the evidence. Tick `prelaunch.qa_pass` only when every check that applies passed (fixed counts), with "qa.md, YYYY-MM-DD" as the evidence; otherwise mark it `[~]` with what's left. Then show me the summary, the guides waiting for me, and the diff.

## Never
- Never ask me to paste a password, key or token into this chat, never write one into a file, never print an environment variable's value.
- Never create accounts, accept terms, pay, or post anything in my name.
- Never delete data, apply migrations to a live database, rewrite git history, or push.
- Never edit TODO.md.
