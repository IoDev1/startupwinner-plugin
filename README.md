# StartUpWinner for Claude Code

Commands for [StartUpWinner](https://start-up-winner.vercel.app), the dashboard that tracks your projects from idea to live on web, iOS and Android. Everything the commands write goes in a `.startupwinner/` folder; your TODO.md is only read.

| Command | What it does |
|---|---|
| `/startupwinner:new` | Starts a new product from the [starter](https://github.com/IoDev1/startupwinner-starter): creates the repo and fills in its name, pitch and dates |
| `/startupwinner:setup` | Sets up the current repo: interviews you and writes everything in `.startupwinner/` (project file, checklist, rules, competitors), plus one line in `CLAUDE.md` |
| `/startupwinner:research` | Researches competitors on the web for the Market tab |
| `/startupwinner:launch` | Writes ready-to-paste launch copy for Product Hunt, Show HN, Reddit and more into `.startupwinner/launch/` |
| `/startupwinner:next` | Works through the checklist on its own and stops only for what needs you, with a step-by-step guide for each stop (accounts, keys, store consoles, decisions) |
| `/startupwinner:plan` | Plans the build before coding: an interview, a spec with a check per step, the data model and access rules, a design file for the look, verification |
| `/startupwinner:qa` | Clicks through the product like a real user before launch and fixes what breaks, a failing test first |
| `/startupwinner:security` | Checks the holes that leak data in AI-built apps and fixes the clear ones |
| `/startupwinner:speed` | Measures, fixes what users feel, and measures again |
| `/startupwinner:focus` | Agrees the one priority for this week with you, from the dashboard's numbers, and records it |

None of them pushes or posts anything; they show you the diff first.

## Install

```bash
claude plugin marketplace add IoDev1/startupwinner-plugin
claude plugin install startupwinner@startupwinner-marketplace
```

Or inside Claude Code: `/plugin marketplace add IoDev1/startupwinner-plugin`, then `/plugin install startupwinner@startupwinner-marketplace`.

## Let your agent read the dashboard

Open https://start-up-winner.vercel.app/settings/agents, create a token and run the `claude mcp add` command it shows, once per computer. Then Claude Code can answer "what should I do today?" from the dashboard (read-only: what's late, what's next, the numbers). `/startupwinner:setup` reminds you at the end.

These files are generated from the prompts the StartUpWinner web app shows; don't edit them here.
