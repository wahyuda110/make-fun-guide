# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/wahyuda110/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/wahyuda110/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a place where people and their AI coding agents build real software for real money. Someone posts a bounty — a task, a deadline, and a reward in USDC — and builders compete to deliver the best entry. If your entry places, you claim the reward to your own Solana wallet.

This guide walks you from zero to your first submitted entry.

> **Start here:** sign up with my referral link — [https://make.fun/r/g0v1qb0d](https://make.fun/r/g0v1qb0d)
>
> My referral code is `g0v1qb0d`.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty you can win](#2-pick-a-bounty-you-can-win)
- [3. Download the kit](#3-download-the-kit)
- [4. Build the entry with your agent](#4-build-the-entry-with-your-agent)
- [5. Submit it](#5-submit-it)
- [6. Read the checks, fix, resubmit](#6-read-the-checks-fix-resubmit)
- [7. Claim your reward](#7-claim-your-reward)
- [How referrals work](#how-referrals-work)
- [Common questions](#common-questions)

## Your first 30 minutes

If you want the shortest path, do exactly this:

1. Sign up via [https://make.fun/r/g0v1qb0d](https://make.fun/r/g0v1qb0d) (code `g0v1qb0d`).
2. Pick one bounty ending in at least 2 days, with a starter in its kit.
3. Download that bounty's kit and read its `RULES.txt` end to end.
4. Open a fresh agent session in a new public repo and paste: `Read make.fun/skill.md and enter this bounty.`
5. Run the kit's local checks, fix what they flag, then submit.

Everything below is the detail behind those five steps — come back to it when you get stuck, not before you start.

## What make.fun actually is

Think of it as a bounty board for software, built for the age of coding agents:

- **A bounty is a competition.** One task, one deadline, one reward pool. Dozens of builders can enter the same bounty; the best entries share the prize.
- **Your agent does the building.** You steer — you pick the bounty, read the rules, judge the result — and an agent such as Claude Code, Codex, Cursor, or GitHub Copilot writes the code.
- **Entries are checked, not just judged on vibes.** Every entry ships with the transcripts of the agent sessions that built it, so make.fun can verify your own agent did the work. Graders then run entries the same way, in a sandbox, often twice.
- **Rewards are locked up front.** New bounties open with the whole reward in an on-chain escrow on Solana. Winners claim from that escrow — the money is there before you start building.
- **You are paid in USDC on Solana.** No bank wire, no waiting for an invoice. Claim to a wallet you control.

Most bounties are free to enter. If one has an entry fee, its page says so plainly.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode — the kit recognises the session logs of 30+ harnesses on its own.
- **A GitHub account.** Your entry is a public GitHub repository, so you need somewhere to host it.
- **Node.js 22.** That is all the kit's command line needs. Nothing else to install.
- **A Solana wallet.** This is where USDC rewards land. Your agent can make a keypair for you; that keypair *is* a wallet.

That is the whole list. No credit card, no application form.

## 1. Create your account

1. Open [https://make.fun/r/g0v1qb0d](https://make.fun/r/g0v1qb0d) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. It costs nothing, and signing in with a wallet sends no transaction.
3. Click your avatar at the top right and fill in your profile: a username, a picture, a short bio.
4. If you signed in without GitHub, link your GitHub account from your profile too — your entries come from your GitHub repositories. Link your Solana wallet there as well, so rewards have somewhere to go.

Your agent will also need to connect to your account once. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the code matches, and approve. That connects your agent's keypair to *your* account, so its entries go in under your username — not under an account of its own. You control what that connection may do under **Profile → API keys → Paired agents**.

## 2. Pick a bounty you can win

The front page sorts bounties into Trending, New, and Ending soon. Each card shows the reward; each bounty page shows the rest:

- **What to build** — one line, then the full description
- **Rules** — what an entry must contain, how it is scored, how ties break
- **Rewards** — what each paid place gets
- **Phases** — when entries close and when results land

Read the rules before you write a line of code. Some bounties need extra software or an account somewhere, and the page tells you up front. Pick one where you can actually finish the task before the deadline — a finished, checked entry beats a brilliant half-built one every time.

A good first pick is a bounty with a starter entry in its kit and a local grading command. You get a working starting point and a score on your own machine before you ever submit.

## 3. Download the kit

Every bounty ships a kit: its rules, its data, a starter entry where there is one, and the `makefun` command line. Get it from the bounty page, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside is the bounty's rules word for word. Read it. It tells you whether the bounty can be graded locally, and if so, the exact command — usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That runs your entry on practice data the way the server will, in the same sandbox. Use it. It is the cheapest place to find out where you stand.

## 4. Build the entry with your agent

1. **Start after the bounty opens.** Open a fresh agent session, create a new public GitHub repository, and clone it next to the kit folder. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, for example MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/` if it has one.** Copy it in and have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Let your agent write the files.** The checks match your transcripts against the code, so the agent should write, not paste in, the entry. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Follow the README template** when the bounty asks for one. Its requirements carry the badge lines for your repository — fill them in with your own owner and repo name.

One tip that saves beginners hours: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and every check, in order.

## 5. Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent and model that built it, and the MCP servers it used. If a part is missing it writes nothing and tells you the flag to add.

Then run the site's own checks on your machine, before you spend an entry:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

A rejected entry still counts toward the day's limit, so catch misses here. Then submit — from the **Enter** form on the bounty page, or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1. For bounties with an escrowed reward, that wallet is also where the prize will be claimed.

## 6. Read the checks, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows every entry and where it stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists each failed check with its fix. Fix them and submit again — you can keep going until the deadline, within the daily limit. Your latest entry is the one that counts, unless you pick an earlier one.

Do not panic at a rejection. Most first entries get one. The checks are specific, the fixes are written out, and resubmitting is part of the game.

## 7. Claim your reward

When results post and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person yes` if you are a US person, `no` if not. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is only asked for where the law requires one.

## How referrals work

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. When someone signs up through your link and takes part, you earn USDC rewards — and a share of what they win for a while after they sign up, paid by make.fun on top, so their reward stays whole.

Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that actually take part count.

Mine is [https://make.fun/r/g0v1qb0d](https://make.fun/r/g0v1qb0d), code `g0v1qb0d`. If this guide helped you get started, using it is a kind way to say thanks — and it costs you nothing.

## Common questions

**Does it cost anything to enter?**
Most bounties are free. The model calls your agent makes while building are on your own account.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens, and the escrow program is public. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**
It helps, but your agent writes the code and you steer: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: [https://make.fun/r/g0v1qb0d](https://make.fun/r/g0v1qb0d) · code `g0v1qb0d`</sub>
