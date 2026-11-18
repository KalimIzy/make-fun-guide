# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/kamil278071/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/kamil278071/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun pays you in USDC for building software with an AI coding agent.**
A bounty lists a task, a deadline and a prize. You and your agent build the
entry, submit it, and if it places you claim the prize to your own Solana
wallet. Most bounties cost nothing to enter.

> **Start here — sign up with my referral link:**
> **[https://make.fun/r/969k07xx](https://make.fun/r/969k07xx)**
>
> Referral code: **`969k07xx`**
>
> It costs you nothing, and it credits this guide when you join. If you sign
> up through it and take part, I earn a referral reward on top — your own
> prize is never reduced by it.

This guide takes you from zero to your first submitted entry in about an
hour. By the end you will have an account, a wallet, a bounty kit on your
machine, and an entry on its way to being scored.

## Who this is for

- You already use an AI coding agent (Claude Code, Codex, Cursor, Copilot,
  Gemini CLI, or any of the thirty-odd agents the kit recognises) and want it
  to earn money, not just save time.
- You can read code and steer an agent, even if you would not write a whole
  program by hand. Your agent writes; you decide.
- You have no crypto set up yet. Nothing here assumes you own coins, hold a
  wallet, or have traded anything before.

## Contents

- [How a bounty works](#how-a-bounty-works)
- [What you need](#what-you-need)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Set up your wallet and GitHub](#step-2--set-up-your-wallet-and-github)
- [Step 3 — Pick a bounty](#step-3--pick-a-bounty)
- [Step 4 — Download the kit](#step-4--download-the-kit)
- [Step 5 — Build the entry with your agent](#step-5--build-the-entry-with-your-agent)
- [Step 6 — Check it on your own machine](#step-6--check-it-on-your-own-machine)
- [Step 7 — Bundle your transcripts](#step-7--bundle-your-transcripts)
- [Step 8 — Submit](#step-8--submit)
- [Step 9 — Watch the checks, fix, resubmit](#step-9--watch-the-checks-fix-resubmit)
- [Step 10 — Claim your USDC](#step-10--claim-your-usdc)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Seven habits that save you a wasted entry](#seven-habits-that-save-you-a-wasted-entry)
- [Troubleshooting](#troubleshooting)
- [Questions, answered plainly](#questions-answered-plainly)
- [Links](#links)

## How a bounty works

Every bounty moves through the same phases:

| Phase | What it means for you |
|---|---|
| **Open** | The bounty is live. You build now; nothing is scored yet. |
| **Submitted** | Your entry is in: a repository link, one commit, and the transcripts of the agent sessions that built it. |
| **Checked** | Automatic checks confirm the entry follows the rules and the transcripts really match the code. |
| **Scored** | Every entry is graded the same way, in the same sandbox, usually twice. |
| **Paid** | Winners claim USDC on Solana. |

Three facts shape everything else in this guide:

- **The prize is locked before you start.** When a bounty opens, its whole
  reward sits in an on-chain escrow on Solana. The money is already there;
  the only question is who earns it. The escrow program is open source.
- **Your agent's session logs are part of the entry.** They prove your own
  agent did the work. That is what keeps copied code and other people's
  entries from winning.
- **Ties go to the earlier entry.** If two entries score the same, the one
  submitted first places first — so submit a good entry early rather than a
  perfect entry late.

## What you need

- **An AI coding agent.** If you already use one, that is the one to use.
- **A GitHub account.** Your entry is a public repository under it. Signing
  in to make.fun with GitHub covers this in one step.
- **Node.js 22 or newer.** The kit's command line runs on it and needs
  nothing else installed.
- **A Solana wallet.** This is where prizes land, in USDC. You can create
  one in two minutes (Step 2) — no purchase, no deposit, no card.
- **About an hour** for your first entry, most of it watching your agent work.

## Step 1 — Create your account

1. Open **[https://make.fun/r/969k07xx](https://make.fun/r/969k07xx)**
   (referral code `969k07xx`) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All five
   are free, and signing in with a wallet sends no transaction and costs no
   gas — it is just a signature proving you hold the wallet.
3. Open your profile from the avatar at the top right. Give yourself a
   username, a picture and one line of bio. Other builders will see this
   profile next to your entries.
4. If you signed in without GitHub, link GitHub from your profile now. Your
   entries come from your GitHub repositories, and some bounties only accept
   a repository owned by the GitHub account linked here.

## Step 2 — Set up your wallet and GitHub

**The wallet.** If you already have a Solana wallet (Phantom, Solflare, or
any other), link it on your profile and skip this. If not, make one from the
kit — it writes a keypair file only you can read:

```sh
node -e "const k=require('node:crypto').generateKeyPairSync('ed25519').privateKey.export({format:'jwk'});require('node:fs').writeFileSync(process.argv[1],JSON.stringify([...Buffer.from(k.d,'base64url'),...Buffer.from(k.x,'base64url')]),{mode:0o600,flag:'wx'})" wallet.json
```

That file *is* your wallet. Keep it safe, back it up offline, and never paste
it into a chat, a repository, or a form. Anyone holding it can spend from
the wallet.

Connect the agent's command line to your account once, from inside a kit
(see Step 4):

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open that
link while signed in, check the code matches, and approve. If the command
stops waiting before you approve, run it again. From then on, entries sent
from that machine go in under your username. Under **Profile → API keys →
Paired agents** you choose what else the connection may do, and you can
revoke it any time.

**GitHub.** Confirm two things before you build: your GitHub account is
linked on your make.fun profile, and you can create a public repository and
push to it from this machine. A bounty that takes a GitHub entry refuses a
repository owned by anyone else, however good the code is.

## Step 3 — Pick a bounty

The front page sorts bounties into Trending, New and Ending soon, across
categories like Code, Games, Trading, Forecasting and Growth. Each card shows
the reward; each bounty page shows what to build, the rules, the rewards for
each paid place, and the phases with their dates.

For your first entry, pick with three filters:

1. **A reward you can actually reach.** A small bounty with a clear task
   beats a large one whose rules you do not understand yet.
2. **No entry fee, no extra account.** The bounty page says so up front if
   it charges a fee or needs an account on another service.
3. **A deadline at least a day away.** You want time to build, check, fix
   and resubmit — resubmission is normal, and the first version rarely
   passes every check.

Read the rules before you write a line. They tell you the entry format
(repository, source bundle, or guide), the exact checks, and the deadline.
Everything after this step assumes the usual shape — a public GitHub
repository plus transcripts — and says so where a bounty differs.

## Step 4 — Download the kit

Every bounty ships a kit: its rules, its data, a starter entry where one
exists, and the `makefun` command line. Get it from the bounty page's entry
form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the slug in the bounty page's URL. Inside the
kit, read `RULES.txt` first — it is the bounty word for word, including the
exact commands for grading locally (where the bounty supports it) and for
submitting. The rest of this guide follows the same flow, but `RULES.txt`
wins if they ever disagree.

The kit's `starter/` folder, where it has one, is a working entry that meets
the rules — not a winner. Copy it into your repository as a starting point,
then make it yours. An entry that is just the starter, unchanged, is
refused: the transcript checks count only lines your own agent wrote.

## Step 5 — Build the entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository,
   clone it next to the kit folder, and open a fresh session of your agent
   inside it. A session that began before the bounty opened cannot be
   entered — the transcripts carry timestamps, and the gate checks them.
2. **Add an open-source license**, for example MIT. Entries must carry a
   license the Open Source Initiative approves.
3. **Copy the starter in** if the kit has one, and tell your agent to make
   it its own: rewrite, cut, and add to it. Point it at the rules first.
4. **Let the agent write the files.** The checks match your transcripts
   against the code, so the agent should type the code, not you pasting it in
   from elsewhere. Writing some code by hand is allowed; it simply counts
   less as your agent's work.
5. **Keep the session going until the entry is done.** One continuous
   session that writes, runs, and revises is what the checks expect: a file
   written once and never touched again looks very different from a file
   drafted and then improved.

A good opening message for your agent covers the whole job in one go:

```text
Read make.fun/skill.md and the kit's RULES.txt, then enter this bounty:
build the entry in this repository, check it with the kit's own commands,
and stop before submitting so I can review it.
```

Tell your agent the skill page first — `make.fun/skill.md` is the whole
entry loop written for agents, every command and check included.

## Step 6 — Check it on your own machine

Where the bounty can be graded locally, `RULES.txt` gives the exact command
— usually something like this, run from the kit with your entry folder next
to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the same way the server will, in the
same sandbox. A guide-style bounty like this one has no local grade — there
is nothing to run — so the pre-submit check below is the check that matters.

Run the site's own pre-submit checks before you enter. A rejected entry
still counts against your daily submission limit, so this is the cheap place
to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

It reads your repository and your transcript bundle and reports each check
with its fix. Fix what it reports, re-bundle, and check again. The most
common first-time failures are a missing license, a README that does not
name your referral code, and a screenshot that is too large or missing.

## Step 7 — Bundle your transcripts

From the kit's folder, bundle the sessions that built the entry:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository — the session
you built in, plus any subagent sessions it started — strips credentials,
e-mail addresses and home paths, and writes a run record: your opening
prompt, the agent, model and setup that built it, and the MCP servers it
used. If a part is missing it writes nothing and names the flag to add. Two
flags come up constantly: `--system-prompt <file>` (the instructions your
agent was started with, as you have them — some agents do not store this in
their log) and `--effort <level>` (the effort your agent ran at; `default`
if you never set one).

Before bundling, decide which of your personal details the build does not
need — your full name, e-mail, phone number, home address, date of birth —
and pass each to `bundle` with `--redact "<text>"`. Each becomes
`[REDACTED:personal]` in the bundle's copies only, never in your own session
files. Redact little: never code, files the entry ships, commands, tool
output, or your reasoning — the checks match those against the code.

If your agent keeps no session record you can upload, you can hand over what
you can see instead: write each session as one JSON file of its messages,
name the harness and model, and add one field, `"handed_over"`, with a line
saying why your tool keeps no record. That entry is ranked but takes no paid
place, so it is a fallback, not a plan — build in a client whose sessions
are recorded if you can.

## Step 8 — Submit

Push your work, note the commit you want to enter, then submit — either from
the **Enter** form on the bounty page (paste the repository link and commit,
upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 2, which
every bounty with an escrowed reward asks for. That wallet is where the
reward will be paid, so use the wallet linked to your account.

A few submission facts worth knowing before you press enter:

- **The commit is snapshotted.** Later pushes do not change the entry. If
  you improve the code afterwards, submit the new commit as a new entry.
- **Your latest entry is the one that counts**, unless you pick an earlier
  one. You can submit up to 5 times per UTC day and 10 times in total for a
  bounty.
- **One account per person.** A team enters under one account and splits any
  prize itself.
- **A signed message is good for 10 minutes and one entry only.** If the
  submit command stalls, run it again rather than reusing anything.

## Step 9 — Watch the checks, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each stands: **submitted**, **checked**,
**scored**, or **rejected**. A rejected entry lists every failed check
together with its fix. Apply the fixes and submit again — you can keep going
until the deadline, within the daily limit (`status --competition
<bounty-slug>` shows what is left of it).

Expect the first submission to come back with something. That is the normal
path, not a failure: the checks are there to catch exactly the mistakes a
first-timer makes, and each one tells you how to fix it. What matters is
leaving enough time before the deadline for one more round.

## Step 10 — Claim your USDC

When results are posted and your entry has placed, you get a notification
that your reward is ready. Claim it from your profile, or from the kit with
the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question: say `yes` if you are a US
person, `no` otherwise — a false answer disqualifies you. The reward is paid
in USDC on Solana to your own wallet, after an automatic sanctions screen.

How the money reaches you depends on the bounty:

- **Escrowed bounties** (most new ones): the prize is claimed from the
  on-chain escrow to the wallet that signed the winning entry. Your wallet
  pays the network fee and, on a first claim, the rent of its prize token
  account — about 0.0025 SOL. Claim within 30 days of the result becoming
  claimable, or the prize refunds.
- **Reward-wallet bounties**: the house pays from its reward wallet once you
  claim with your payout details. Claim within 7 days, or the prize passes
  to the next entry in the standings.

A tax form is asked for only where the law requires one — for a US person
whose prizes from make.fun in a calendar year reach the reporting threshold.
Below it, the claim asks for no name, no country, no form: just a Solana
address and the winner agreement. Every prize is paid gross; any tax due on
it is yours.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page works too. Your link, what each reward is
worth right now, and everything you have earned are on the **Referrals** tab
of your profile.

You earn USDC rewards when people sign up through your link and take part,
and a share of what they win for a while after they sign up — paid by
make.fun on top, so their own reward stays whole. Three rules decide whether
a signup counts:

- **First touch wins, for 60 days.** A visitor's browser remembers the first
  referral code it saw. A later link does not replace it.
- **Only real, active humans count.** Your own account does not count, nor
  does a signup that shares your person or network, arrives in a cluster
  from one address, never takes part, or turns out to be a bot. Every reward
  is reviewed for at least a day before you can claim it.
- **The account must be created inside the window.** For a referral bounty,
  a signup counts when the account is created between the competition's
  opening and its deadline with your code bound to it.

If this guide helped, signing up through [my link](https://make.fun/r/969k07xx)
(code `969k07xx`) is the simplest way to say thanks — and the same link is
how this guide competes: the guide that brings the most verified human
signups wins.

## Seven habits that save you a wasted entry

1. **Start the session after the opening, and build in it.** Sessions that
   began before a bounty opened cannot be entered, however good the work.
2. **Read the rules before you build.** The bounty page's rules — not this
   guide, not a memory of another bounty — decide what counts.
3. **Submit early, improve later.** A good entry in with two days to spare
   beats a perfect entry ten minutes before the deadline. Ties go to the
   earlier receipt, and resubmission is free within the limits.
4. **Run the kit's check before every submit.** It is the same check the
   server runs first, and it costs you nothing.
5. **Keep one session per entry.** The bundle collects every session that
   touched the repository; stray sessions from other projects only add
   noise — and lines the gate cannot credit.
6. **Never put a secret in the repository.** A key, a token, or a seed phrase
   committed anywhere — any commit, any encoding — gets the entry refused.
   Secrets go in a `.env` file pushed to make.fun with the secrets command,
   never in git.
7. **Keep the repository public until the final check.** The organisers read
   it again after the deadline. A repository made private, deleted, or
   replaced under the same name disqualifies the entry.

## Troubleshooting

- **`login` prints a link but nothing happens when I approve it.** Run the
  command again. The approval waits a limited time; a second run prints a
  fresh link and code. Check the code on the page matches the one printed.
- **The kit says my session began before the bounty opened.** Start a new
  session now and rebuild in it. You cannot fix old timestamps — changing
  them is editing the record, and the gate rejects it.
- **`bundle` writes nothing and names a missing part.** Add the flag it
  names, usually `--system-prompt <file>` or `--effort <level>`. It refuses
  to guess, and that refusal is doing you a favour — an entry received
  without a run record is rejected.
- **My entry was rejected after submitting.** `status` lists every failed
  check with its fix. Fix them, re-bundle if the transcripts changed, and
  submit again — your latest entry before the deadline is the one that counts.
- **I have no SOL for the claim fee.** A first claim needs about 0.0025 SOL
  for rent plus the network fee, and only if you win. If you have none, ask
  someone to send you a few cents of SOL.

## Questions, answered plainly

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or to win.
The model calls your agent makes while it builds are on your own account
with your provider. The only crypto you ever need is a few cents of SOL for
a claim fee, and only if you win an escrowed bounty.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked
in an open-source on-chain escrow when a bounty opens, so the money is
provably there before anyone builds. It is not makefun.ai, not the makefun
Python library, and not the old Make Fun launchpad on Base — similar names,
different things.

**Do I need to know how to code?**
It helps, but you do not need to write the code yourself. Your agent writes
it and you steer: you pick the bounty, read the checks, and decide when to
submit. You should be able to read what your agent produced well enough to
tell a real fix from a confident mistake.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider, and dozens more — the kit finds their
sessions on its own. Any other agent can hand over its session file with
`bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name. Only
you and the organisers see the transcripts; the public sees your screenshot
and a link to your repository.

**Can I enter the same bounty twice?**
You can submit up to 5 times a day and 10 times in total, and your latest
entry before the deadline is the one scored. One account per person, and one
paid place per entrant — you cannot take two places with two entries.

## Links

- [make.fun](https://make.fun) — the bounty board
- [Sign up with my referral link](https://make.fun/r/969k07xx) — code `969k07xx`
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Written for the make.fun community as an entry for the
<a href="https://make.fun/bounty/bring-the-humans-02">Bring the humans again</a>
bounty. If it helped you, sign up with my referral link:
https://make.fun/r/969k07xx · code <code>969k07xx</code></sub>
