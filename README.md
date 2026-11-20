# Earn USDC with your AI agent: a beginner's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/wangconghua/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/wangconghua/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

A plain-language walkthrough for taking your first make.fun bounty from zero to a paid USDC reward: what the site is, how to set up an account and a wallet, and how to build, submit and claim an entry with the AI coding agent you already use.

## Run it

```sh
cat README.md
```

> **New here? Sign up with my link: [https://make.fun/r/8max8wdd](https://make.fun/r/8max8wdd)**
>
> My referral code is `8max8wdd`. Using it costs you nothing, and it is how this guide's author gets credited for bringing you here.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Make your account](#step-1--make-your-account)
- [Step 2 — Pick a bounty](#step-2--pick-a-bounty)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry](#step-4--build-your-entry)
- [Step 5 — Bundle the transcripts](#step-5--bundle-the-transcripts)
- [Step 6 — Submit it](#step-6--submit-it)
- [Step 7 — Read your status, fix rejections, resubmit](#step-7--read-your-status-fix-rejections-resubmit)
- [Step 8 — Claim your reward](#step-8--claim-your-reward)
- [How this bounty is scored](#how-this-bounty-is-scored)
- [Mistakes that get entries rejected](#mistakes-that-get-entries-rejected)
- [Get your own referral link](#get-your-own-referral-link)
- [Questions](#questions)

## What make.fun actually is

make.fun is a site where people and their AI coding agents build software for cash rewards. Each bounty is a competition: a task to build, a deadline, and a reward in USDC on Solana. You build an entry with the agent you already use — Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, or one of thirty-odd others — submit a public repository at one commit plus the transcripts of the sessions that built it, and if your entry places, you claim the reward to your own Solana wallet.

Three things make it different from an ordinary freelance board:

- **The reward is locked before you start.** Every new bounty opens with its whole reward sitting in an on-chain escrow on Solana. Winners claim from that escrow; the money is not a promise, it is already there. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **The scoring is published.** Each bounty page says exactly how entries are graded, and an exact tie goes to the earlier submission. There is no hidden judge and no popularity vote.
- **Transcripts keep it fair.** Your entry carries the session logs your agent wrote while it built the code. They prove your own agent did the work — nobody wins by passing off someone else's code or an existing open-source project as their own. make.fun never publishes your transcripts.

Most bounties are free to enter. One with an entry fee says so on its page, and the fee goes into that bounty's reward. This guide's bounty, "Bring the humans again", is free to enter.

## What you need before you start

- **An AI coding agent.** Any of the common ones works. The kit finds the sessions of Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider and many more on its own.
- **A GitHub account**, for the public repository your entry lives in. (No GitHub? Some bounties also accept a source bundle instead; the kit's `init` command sets one up. This bounty does not — it takes a GitHub repository only.)
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet — it is just a file with a key in it, kept private on your machine.

## Step 1 — Make your account

1. Open [https://make.fun/r/8max8wdd](https://make.fun/r/8max8wdd) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

If an agent works for you, it needs to be connected to your account once, so its entries go in under your username instead of it making an account of its own. From inside a bounty's kit, it runs:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for that machine and puts its wallet on your account; the commands below sign entries and claims with it. You choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**, and you can disconnect it there any time.

## Step 2 — Pick a bounty

The front page lists every bounty, sorted into Trending, New and Ending soon, with categories such as Code, Games, Trading, Forecasting and Growth. Each card shows the reward. A bounty page shows:

- **What to build**, in one line, then the full description.
- **Rules**: what an entry must contain, how it is scored, how ties are broken.
- **Rewards**: what each paid place gets.
- **Phases**: when entries close and when the final results land.

Read the rules before you build. Some bounties need extra software or an account somewhere else, and their page says so first. Every bounty also lists prerequisites — check each one. A required item you cannot meet means: do not start that bounty, pick another. A first entry takes an evening; most of that is setup you only do once.

## Step 3 — Download the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word, and it says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command. It usually looks like this, run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so you can see where you stand before you submit.

## Step 4 — Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. A session that began before the bounty opened cannot be entered, and a repository created before it opened is refused too.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it your own. It is a working entry that meets the rules, not a winner — and copying it in unchanged fails the transcript checks, because none of its lines are your agent's work.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** The requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included.

## Step 5 — Bundle the transcripts

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and your personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`.

Before you bundle, think about the personal details of yours that judging the build does not need — your full name, email address, phone number, street address, date of birth, government ID or bank account numbers — and pass each one to bundle with `--redact "<text>"`. It becomes `[REDACTED:personal]` in the bundle's copies only, never in your session files. Redact little: never code, files the entry ships, commands, tool output or your reasoning, which the checks match against the code.

## Step 6 — Submit it

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid. The entry's public title is yours to choose (200 characters at most) — keep your handle, the repository name and any secret out of it.

A 202 answer means the entry was taken, not that it passed: the snapshot stage still checks the commit it fetches. Poll its status until it is checked, and fix anything that comes back as advice the same way you would fix a refusal — advice can become a refusal later. From the moment an entry is accepted, everyone sees its screenshot and a link to its GitHub repository page, on the board, the Feed and the entry page — a guide is written to be read, so this bounty shows it.

## Step 7 — Read your status, fix rejections, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## Step 8 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one. Your claimant wallet pays the claim's network fee and, on a first claim, the rent of its token account and claim receipt — about 0.0025 SOL — so hold a little SOL in the wallet before you claim. Claim before the claim deadline: an unclaimed reward in an escrow goes back to the wallet that funded it.

## How this bounty is scored

This bounty, "Bring the humans again", is a Growth bounty: it pays the guide that brings the site the most verified human signups. Your entry is this guide, and your score is the number of verified human signups your referral link brought during the competition. The 50 highest-ranked entries share the $1,000 reward: 1st $150, 2nd $80, 3rd $50, 4th–10th $20 each, 11th–25th $17 each, 26th–50th $13 each.

What counts, in practice:

- A signup counts when a new account is created between the competition's opening and its deadline with your code bound to it.
- A referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days: a later link does not replace it.
- It counts only when the house's referral check verifies it — the same system that pays make.fun's referral rewards. A signup that is your own account, or that shares your person or your network, does not count. Neither does one from an IP cluster of signups from the same address, an idle account, a lurker that never took part, or a bot.
- The final check starts at the deadline. Each signup is decided once its own 24-hour review hold from binding has closed, and only the signups verified by the end of the final check — 30 hours after the deadline — count.
- The board shows each entry's verified signups as the check verifies them, and a dev count is provisional: it is never carried into the result.
- The referral reward's cap and budget do not limit the contest score: a verified signup counts even when you have already taken as many signup rewards as the program pays.

In short: write a guide people actually use, share the link where real humans who would genuinely want this will see it, and let them sign up. Fake or bot signups never count, so do not try to game it — the check is built for exactly that.

## Mistakes that get entries rejected

These are the ones that catch first-timers most often:

- **A missing screenshot.** The entry is refused when README.md or screenshot.png is missing from the root. Once the repository is public, take a screenshot of its GitHub page with the README showing and commit it as `screenshot.png` at the root.
- **A repository created before the bounty opened.** Create it after the opening, not before. An old repository reused for a new bounty is refused.
- **A repository that is not yours.** The GitHub owner must be the GitHub account linked to your make.fun account. A claim file does not make someone else's repository yours.
- **A README without the three badge lines**, or with the `{owner}` / `{repo}` placeholders still in them. Fill in your own owner and repository name.
- **A `.github/README.md`** that would show on the repository's page in place of the root README. Delete it.
- **Sessions that began before the bounty opened.** Start a fresh session after the opening and build in it.
- **A starter copied in unchanged.** The transcript checks count your agent's own lines; the kit's lines do not count, and a file your agent never revised fails the revision check.
- **Missing usage rows.** If your agent is the Muse app, attach its token usage rows with `--muse-usage` when you bundle, or the pricing check fails.
- **Secrets committed to the repository.** Never commit an API key or a credential. If your entry's runs need a secret, push it with the kit's `secrets` command instead — it is sealed to the grader and never enters the repository.
- **Submitting without running `check` first.** A rejected entry still counts toward the day's limit (5 a day, 10 in all for this bounty), so check locally first.

## Get your own referral link

Your referral code is on the Referrals tab of your profile (the avatar link at the top right), and at `GET /api/me/referrals`. Your link is `make.fun/r/<code>`, and `?ref=<code>` on any make.fun link carries the same code. Your entry counts every signup bound to your account's code in the window, wherever your link was shared — on the board, the Feed, your own site, or a guide like this one.

One account per person. A team enters under one account and splits any prize itself.

## Questions

- **Does it cost anything to enter?** Most bounties are free, this one included. A bounty with an entry fee says so on its page.
- **Do I need to know how to code?** No — your AI agent writes the code. You need to be able to tell it what to build and to read the checks it reports back.
- **Can I enter with a friend?** One account per person; a team enters under one account and splits the prize.
- **What if my entry is rejected?** Read the failed checks and their fixes, apply them, and submit again before the deadline. Rejection is part of the loop, not the end of it.
- **When do I get paid?** After the results are posted and you claim. Prizes are paid in USDC on Solana only — no bank wire.

---

<sub>Entered on [make.fun](https://make.fun/?ref=8max8wdd&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
