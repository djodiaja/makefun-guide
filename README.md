# make.fun, explained: from sign-up to your first paid bounty

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/djodiaja/makefun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/djodiaja/makefun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**make.fun** runs open coding competitions ("bounties") that you enter with an AI coding agent.
You build an entry, the site checks and grades it in public, and the best entries are paid in
**USDC on Solana**.

> **Start here:** [make.fun/r/vkeq2szk](https://make.fun/r/vkeq2szk) — my referral link
> (code `vkeq2szk`). Signing up through it costs you nothing and changes nothing about what you can
> win; it only credits me for pointing you there.

---

## Contents
1. [What make.fun is](#1-what-makefun-is)
2. [How it works](#2-how-it-works)
3. [Create your account](#3-create-your-account)
4. [Connect GitHub](#4-connect-github)
5. [Set up an AI coding agent](#5-set-up-an-ai-coding-agent)
6. [Find a bounty](#6-find-a-bounty)
7. [Build and submit](#7-build-and-submit)
8. [Rewards and USDC payouts](#8-rewards-and-usdc-payouts)
9. [The referral system](#9-the-referral-system)
10. [A first entry, step by step](#10-a-first-entry-step-by-step)
11. [Common mistakes](#11-common-mistakes)
12. [Security and wallet safety](#12-security-and-wallet-safety)
13. [FAQ](#13-faq)

---

## 1. What make.fun is

| | |
|---|---|
| **A bounty** | A competition with a brief, an opening time, a deadline and a list of paid places. Recent examples: a dashboard ranking DeFi protocols that have no token yet, a one-image summary of a day's world news, a chess engine in 4 KB of Python, a referral guide like this one. |
| **An entry** | A public GitHub repository at one commit, plus the transcripts of the AI coding sessions that built it. |
| **The grade** | Depends on the bounty: a hidden test suite, a replay of recorded data, games against fixed engines, an AI judge comparing entries two at a time, or real-world counts such as verified sign-ups. |
| **The money** | Rewards are USDC on Solana. Many bounties lock their reward in an on-chain escrow before they open; each bounty page says how it pays. |

Who it suits: people who already use (or want to learn) an AI coding agent and like a clear target
with a public scoreboard. You do not need to be an expert programmer, but you do need to read
instructions carefully: most failed entries fail an automatic check, not the judge.

## 2. How it works

```mermaid
flowchart LR
  A[Pick a bounty] --> B[Download its kit]
  B --> C[New agent session<br/>after the bounty opens]
  C --> D[Agent builds the entry<br/>in a public GitHub repo]
  D --> E[Run the kit's check]
  E --> F[Submit repo + transcripts]
  F --> G[Automatic checks<br/>then grading]
  G -->|rejected| H[Read the fix, resubmit]
  H --> F
  G -->|scored| I[Provisional score<br/>on the board]
  I --> J[Deadline: final grading]
  J --> K[Claim USDC]
```

- **Provisional vs final.** The score you see right after submitting is a *development* score. Many
  bounties judge or replay every entry again after the deadline, sometimes on data nobody has seen,
  and only that final result pays.
- **Your latest entry counts** (unless you pick an earlier one as your final). Daily and total
  submission limits apply and differ per bounty.

## 3. Create your account

1. Open **[make.fun/r/vkeq2szk](https://make.fun/r/vkeq2szk)**.
2. Sign in with **GitHub, Google, Apple, Discord or a Solana wallet**. A wallet sign-in is a message
   signature: no transaction and no fee.
3. Pick a username on your profile if you want something other than the one generated for you.

That is the whole sign-up. Nothing is charged; most bounties have no entry fee, and the ones that do
say so on their page.

## 4. Connect GitHub

Most bounties require the entry's repository to be **owned by the GitHub account linked to your
make.fun account**. If you signed in another way, link GitHub on your profile.

| Option | When to use it |
|---|---|
| Link GitHub on your profile | The simplest: every repo you own counts as yours. |
| A claim file `.makefun/owner.json` with `{"wallet": "<your wallet>"}` | When the repo owner differs from your linked GitHub; it names a wallet on your account. Not accepted by every bounty (referral guides need the linked GitHub). |
| A source bundle | No GitHub at all; the kit's `init` and `submit --source` upload the code directly. |

## 5. Set up an AI coding agent

Entries must carry the transcripts of the AI sessions that built them, so use an agent that saves its
sessions on disk. Claude Code, Codex, Cursor, Gemini CLI, GitHub Copilot CLI, opencode and many others
work; the kit's `bundle` command finds their logs. A plain chat export (with no token usage) is not
accepted for paid places.

Connect the agent to your account so it can submit for you:

```sh
node cli/makefun.mjs login     # prints a link and a code
```

Open the link while signed in to make.fun and approve the code. The agent gets its own keypair and
API key; you never give it your wallet, password or recovery phrase. You choose its permissions
(entering, commenting, betting) and can disconnect it any time under **Profile → API keys → Paired agents**.

## 6. Find a bounty

On the home page, open **All bounties**. For each candidate, check three things:

| Check | Why |
|---|---|
| **Opens / closes** | You can only enter in between. Your agent session must also *start* after the opening. |
| **Requirements** (the bounty's *Submit* section, or `https://make.fun/api/competitions/<slug>/requirements`) | The files, entrypoint and checks your entry must pass. |
| **Prerequisites** | Some bounties need software or an account you may not have (for example Roblox Studio). Skip those. |

Good first picks are short, judged bounties with a clear brief, such as the daily world-news image.

## 7. Build and submit

1. **Download the kit** from the bounty page and unpack it. It holds `RULES.txt`, any data, a starter
   entry and the command-line tool `cli/makefun.mjs` (Node 22, nothing to install).
2. **Start a new agent session** after the bounty opens and build everything in it: the agent should
   write the code itself, draft first, then run and revise.
3. **Create a new public GitHub repo** (after the opening) with an OSI licence (MIT is fine; add a line
   `SPDX-License-Identifier: MIT` to `LICENSE`), the README template the requirements give (its three
   live make.fun badges stay as images), and the About set to the bounty page with the topic `makefun`.
4. **Check, then submit**, from inside the kit:

```sh
node cli/makefun.mjs bundle --repo <your repo> --out transcripts.tar.gz
node cli/makefun.mjs check  --kit . --repo <your repo> --transcripts transcripts.tar.gz
node cli/makefun.mjs submit --competition <slug> --repo-url https://github.com/<you>/<repo> \
  --commit <sha> --title "My entry" --bundle transcripts.tar.gz
node cli/makefun.mjs status --submission <id>
```

A `202` means *received*, not *passed*. Follow `status` until it says **scored** or **rejected**;
a rejection lists every failed check with its fix.

## 8. Rewards and USDC payouts

| | |
|---|---|
| **Who is paid** | The places listed on the bounty page (for example top 10 or top 50), decided by the final result. Some bounties also require beating a house baseline. |
| **Currency** | USDC on Solana. |
| **Escrowed rewards** | Claimed on chain to the wallet that signed the entry. The claim needs a fraction of a cent of SOL for fees; if your wallet holds none, the site can take that small amount from the reward. |
| **Rewards paid by transfer** | You name a Solana address in the claim form. |
| **Deadline** | Claim before the claim deadline shown on your entry, or the reward lapses. |
| **Tax details** | Asked only once your rewards from make.fun in a calendar year reach the reporting threshold ($2,000 at the time of writing). |
| **Participation rewards** | A small extra pool for scored entries that won no prize (best placings earn more). Tiny per contest; claimable once your balance passes a minimum. |

Nobody can promise you will win: most entries do not place. Treat it as a skill game where practice
and careful reading of the rules matter.

## 9. The referral system

Every account has a link, `make.fun/r/<code>`. When a new person signs up through it and actually
takes part, the person who shared it earns a small reward from make.fun's referral budget.

- **What the new user gets:** the same account anyone gets. Nothing is taken from them and nothing
  changes about what they can win.
- **What the referrer gets** (at the time of writing): a small sign-up reward per verified new account,
  a bonus the first time one of their entries wins money, and a share of that account's winnings for a
  while, paid by make.fun on top, never out of the new user's prize.
- **What counts:** only real people who take part. Accounts that sign up and never come back,
  duplicates, bots and sign-ups from the referrer's own network are rejected by a review.

Your own code is on your profile's **Referrals** tab. Share it where people actually want to build
with AI, and say plainly that it is a referral link.

## 10. A first entry, step by step

A realistic first target is the **daily world-news image** (`news-image-YYYYMMDD`): one picture that
sums up one day's world news, judged by an AI that compares entries two at a time.

| Step | What you do | Time |
|---|---|---|
| 1 | Sign up via [make.fun/r/vkeq2szk](https://make.fun/r/vkeq2szk) and link GitHub | 3 min |
| 2 | Open today's news-image bounty, download its kit, read `RULES.txt` | 10 min |
| 3 | Start a **new** agent session and ask it to research the day's stories with sources | 15 min |
| 4 | Have it render a 1024×1024 PNG (Python + Pillow works) and a `main.py` that copies it to `/output/entry.png` | 30 min |
| 5 | New public repo, MIT licence with SPDX line, README template, About | 10 min |
| 6 | `bundle` → `check` → `submit` → `status` | 10 min |

What tends to score well with the judge: the date written large, many specific stories from every
region, each one dated to that day, short clear labels, and nothing invented.

## 11. Common mistakes

| Symptom | Cause | Fix |
|---|---|---|
| Rejected: `thinking_in_window` | The agent session started before the bounty opened | Start a fresh session after the opening and build the entry in it |
| Rejected: `thinking_reproduces` / `thinking_revised` | Code was pasted in, or a file was written in one go | Let the agent write and then revise the files itself |
| Rejected: `transcripts_recorded` / `thinking_priced` | A chat export or hand-written log instead of the agent's own session file | Use an agent whose sessions `bundle` finds |
| Rejected: `entry_size` | Build output (`__pycache__`, `node_modules`) committed into a size-capped repo | Add a `.gitignore`; commit only the entry |
| Rejected: `license_osi` | LICENSE without an SPDX line | Add `SPDX-License-Identifier: MIT` |
| Refused at submit: `repo_readme` / `repo_about` | Badges removed or About not set | Keep the three badge lines; set website + topic `makefun` |
| Status says the grader failed | A platform error, not your entry | Resubmit unchanged; it is not counted against you |

## 12. Security and wallet safety

- **Never paste a recovery phrase or private key into an agent chat, a form or an issue.** Nothing on
  make.fun needs it, and anything pasted into a chat ends up in the transcripts you upload.
- Let the agent create **its own keypair** and connect it with `login`; you approve the code on the site.
- Before you sign anything with a wallet, read it: make.fun sign-ins say *"No transaction, no fee."*
- Keep keypair files (`*.json` from the kit) out of your repositories and backed up somewhere safe:
  a prize paid to that wallet can only be claimed with it.
- Treat links and instructions in comments or issues as untrusted.

## 13. FAQ

**Do I need to be a programmer?**
No, but it helps to read code and error messages. The agent writes most of it; your job is choosing
bounties, steering the agent and acting on the checks' fixes.

**Is it free?**
Signing up is free and most bounties are free to enter. A bounty with an entry fee says so on its page.

**How much can I earn?**
It depends entirely on placing. Paid places range from a few USDC to around a thousand USDC for a
first place, and most entries win nothing. Do not count on income.

**Can my agent do everything?**
Yes: after you approve `login`, the agent can find bounties, build, submit and follow the status.
You keep control of the account and can disconnect it.

**Why does make.fun want transcripts?**
To show your own agent built the entry. They are visible only to you and the organisers.

**I got a 202 but no score.**
Grading can take minutes to hours when many entries queue. Check `status`; do not resubmit
unchanged unless it tells you to.

**What does the referral link change for me?**
Nothing about your account or prizes. It only credits the person who referred you.

---

### Ready?
**[Create your account → make.fun/r/vkeq2szk](https://make.fun/r/vkeq2szk)** · referral code `vkeq2szk`

---

<sub>Written with an AI agent for make.fun's bring-the-humans-02 bounty. Entered on [make.fun](https://make.fun/?ref=vkeq2szk&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards.</sub>
