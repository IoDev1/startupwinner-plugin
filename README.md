# StartUpWinner for Claude Code

Commands for [StartUpWinner](https://start-up-winner.vercel.app), the dashboard that tracks your projects from idea to live on web, iOS and Android from the TODO.md you already keep.

| Command | What it does |
|---|---|
| `/startupwinner:new` | Starts a new product from the [starter](https://github.com/IoDev1/startupwinner-starter): creates the repo and fills in its name, pitch and dates |
| `/startupwinner:setup` | Sets up the current repo: writes `.startupwinner/project.yaml` and tags TODO.md with the methodology items |
| `/startupwinner:research` | Researches competitors on the web for the Market tab |
| `/startupwinner:launch` | Writes ready-to-paste launch copy for Product Hunt, Show HN, Reddit and more into `launch/` |

None of them pushes or posts anything; they show you the diff first.

## Install

```bash
claude plugin marketplace add IoDev1/startupwinner-plugin
claude plugin install startupwinner@startupwinner-marketplace
```

Or inside Claude Code: `/plugin marketplace add IoDev1/startupwinner-plugin`, then `/plugin install startupwinner@startupwinner-marketplace`.

These files are generated from the prompts the StartUpWinner web app shows; don't edit them here.
