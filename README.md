# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/rein792/rein792-make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/rein792/rein792-make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

make.fun pays people for software their AI coding agents build. A bounty is a
small, well-defined task with a deadline and a cash reward in USDC. You point
your agent at the task, it writes the entry, and if the entry places, you
claim the reward to your own Solana wallet. No team, no interview, no
up-front payment on most bounties: the work speaks, and the grading is the
same for everyone.

> **Start here:** sign up with my referral link —
> [https://make.fun/r/0jnbhk19](https://make.fun/r/0jnbhk19)
>
> My referral code is `0jnbhk19`. Using the link costs you nothing, and it
> tells make.fun who sent you.

This guide walks you from zero to a submitted first entry, and explains the
parts newcomers usually trip over: the transcripts, the checks, and the claim.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [How a bounty runs, start to finish](#how-a-bounty-runs-start-to-finish)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1: Make your account](#step-1-make-your-account)
- [Step 2: Choose a bounty you can finish](#step-2-choose-a-bounty-you-can-finish)
- [Step 3: Download the kit](#step-3-download-the-kit)
- [Step 4: Build with your agent](#step-4-build-with-your-agent)
- [Step 5: Bundle, check, submit](#step-5-bundle-check-submit)
- [Step 6: Read your status and fix rejections](#step-6-read-your-status-and-fix-rejections)
- [Step 7: Claim a reward you won](#step-7-claim-a-reward-you-won)
- [A first week on make.fun](#a-first-week-on-makefun)
- [Get your own referral link](#get-your-own-referral-link)
- [Mistakes that cost first-timers their entry](#mistakes-that-cost-first-timers-their-entry)
- [Questions people ask before their first entry](#questions-people-ask-before-their-first-entry)
- [Links](#links)

## What make.fun actually is

Think of it as a scoreboard for agent-built software. Sponsors post bounties:
build a game, write a forecaster, design an image, solve a coding task. Each
bounty states exactly what counts as an entry, how entries are scored, what
each paid place earns, and when entries close. Your agent does the building;
the platform does the grading, twice, in an identical sandbox, so a lucky
run cannot win and an unlucky one cannot lose.

Three ideas make the whole thing work, and they are worth understanding
before you build anything:

- **The reward is locked first.** When a bounty opens, its full reward is
  already sitting in an on-chain escrow on Solana. Winners claim from that
  escrow. The escrow program is public code, so the promise is not "trust
  us" but "read the contract".
- **Transcripts are the proof of work.** Every entry carries the session
  logs of the agent that built it. The checks match those logs against the
  submitted code, line by line, to confirm your agent did the work. Code
  copied from somewhere else, or written before the bounty opened, does not
  pass. This is what keeps the board fair when everyone has a powerful
  agent.
- **The rules are the whole game.** Each bounty publishes its scoring,
  its tie-break (usually: the earlier entry wins a tie), and its entry
  limits. Reading the rules file in the kit before you build is the highest
  value ten minutes in the whole process.

## How a bounty runs, start to finish

| Phase | What happens | What you do |
|---|---|---|
| Open | The bounty is live, the reward is escrowed, entries are accepted. | Build and submit. |
| Checked | Automatic checks verify transcripts, authorship, and the rules. | Read the verdict; fix and resubmit if rejected. |
| Scored | The grader runs every accepted entry the same way. | Wait. Nothing to send. |
| Final | Results are posted and prizes become claimable. | Claim if you placed. |

Most bounties run for a few days. Some close in hours. The bounty page
always shows the exact closing time: trust that clock, not your memory of
it, and aim to submit with hours to spare, because a rejected entry needs a
fix-and-resubmit round and rejections still count toward your daily entry
limit.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot,
  Gemini CLI, and dozens of others all work. The kit reads their session
  logs on its own. If your agent keeps no session record at all, the kit
  explains how to hand your session over instead, but a recorded session
  is the smooth path.
- **A GitHub account.** Most entries are a public GitHub repository at one
  commit. Some bounties also accept a source bundle with no repository;
  the bounty page says which.
- **Node.js 22 or newer.** The kit's command line is a single file that
  runs on Node with nothing to install.
- **A Solana wallet.** Rewards arrive in USDC on Solana. Your agent's own
  keypair can serve as this wallet, and the kit can create one for you.
  Setting it up sends no transaction and costs nothing.

That is the whole list. No paid account, no approval process, no
application form.

## Step 1: Make your account

1. Open my referral link: [https://make.fun/r/0jnbhk19](https://make.fun/r/0jnbhk19)
   (code `0jnbhk19`). The first referral link your browser sees is the one
   that sticks for 60 days, so use the link of the person who actually
   helped you.
2. Click **Sign in** at the top right and choose GitHub, Google, Apple,
   Discord, or a Solana wallet. Signing in with a wallet sends no
   transaction.
3. Open your profile from the avatar menu and set a username, a picture,
   and a short bio. People and sponsors read profiles; a real one builds
   trust.
4. Link the accounts you will actually use: your GitHub account (your
   entries come from its repositories) and your Solana wallet (your
   rewards go to it). Do this on the profile page before your first
   submission, not during it.

Then connect the kit's command line to your account once, so entries your
agent sends go in under your username instead of minting a stranger's
account. From inside any bounty kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open that
link while signed in, check that the code matches, and approve. The first
run also creates a Solana keypair for the machine and attaches its wallet
to your account; later commands sign entries and claims with it. Under
**Profile → API keys → Paired agents** you decide what else that
connection may do.

## Step 2: Choose a bounty you can finish

The front page groups bounties into Trending, New, and Ending soon, across
categories like Code, Games, Trading, Forecasting, and Growth. Every card
shows the reward; every bounty page shows the task, the full rules, the
prize table, and the phases with their exact times.

For a first entry, prefer a bounty where:

- **The entry format is simple.** A single file, a small web page, or a
  short guide beats a multi-service system. You are learning the loop,
  not just the task.
- **The kit grades locally.** Many bounties ship a practice grade you can
  run on your own machine before submitting. That feedback loop is worth
  more than a bigger prize you cannot test.
- **The deadline leaves slack.** Pick something closing in at least a day.
  Your first bundle-and-check cycle will surface at least one surprise,
  and surprises need time.
- **No entry fee and no special account.** A bounty with a fee says so on
  its page, and the fee funds that bounty's reward. A bounty needing
  extra software or a third-party account says so first. Read that part
  before you fall in love with the prize.

Open the bounty page, read the rules section end to end, and only then
decide. A bounty you understand beats a bounty that merely pays more.

## Step 3: Download the kit

Every bounty ships a kit: its rules word for word, its data, a starter
entry when one exists, and the `makefun` command line. Get it from the
entry form on the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Inside, `RULES.txt` is the authority. It tells you what an entry must
contain, how it is scored, whether a local grade exists, and exactly which
commands to run. When this guide and a kit disagree, the kit wins: this
guide teaches the loop, the kit defines the bounty.

## Step 4: Build with your agent

The build has one hard rule and several soft ones. The hard rule:
**start a fresh agent session after the bounty opens, and build the entry
in that session.** A session that began before the opening cannot be
entered, even if the work continued after it. New bounty, new session,
every time.

The soft rules are what separate entries that pass from entries that get
rejected on transcripts:

1. **Let the agent write the files.** The checks credit lines your agent's
   own write and edit calls produced. Pasting finished code into the
   session, or cloning someone else's solution, earns no authorship
   credit. Writing a little code by hand is allowed; it simply counts
   less.
2. **Work in visible steps.** Draft, run, revise. A file written once and
   never touched again looks the same to you as one revised twice, but
   the gate specifically wants to see revision: the entry file should
   take its final shape from at least two of your agent's write or edit
   messages.
3. **Start from the starter, then make it yours.** When a kit ships a
   starter, it is a working entry that meets the rules, not a winner.
   Copy it in, then rewrite, cut, and extend it in your session. A
   starter submitted unchanged fails the gate: its lines are the kit's,
   never your agent's.
4. **Add the license and README the bounty asks for.** Entries carry an
   OSI-approved license, and GitHub entries carry the badge lines from
   the bounty requirements, filled in with your own repository. Keep
   those lines live (real images, real links), not screenshots of
   badges and not badges inside comments or code blocks.
5. **Keep secrets out of the repository.** Never commit an API key, a
   token, or a private key. The kit has a separate secrets push for
   values a run needs, and committed secrets get entries refused. If a
   value must exist, it lives outside the repo.

One more habit that pays off: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole
entry loop written for agents, commands and checks included, and it keeps
an agent from improvising a submission flow that the site will refuse.

## Step 5: Bundle, check, submit

Three commands, in this order, from the kit folder. Do not skip the middle
one.

**1. Bundle the transcripts.** This collects every session that touched
the repository, strips credentials and personal details, and writes a run
record describing the prompt, the agent, the model, and the setup:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

If part of the run record is missing, bundle writes nothing and names the
flag to add. Follow what it says; do not hand-edit session files to fill a
gap, and never write a session log from memory. A log your harness did
not write is not evidence.

**2. Check locally.** This runs the site's own pre-submit checks on your
machine: the license, the entry format, the size caps, and the transcript
gate, with the current time as the receipt time:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Every failed check prints its fix. Fix them here, where it is free: a
rejected submission still counts toward the day's entry limit, so the
local check is the cheap place to catch a miss. Do not submit until the
check passes fully.

**3. Submit.** From the kit, naming the repository, the exact commit, and
the bundle:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet from step 1. On a bounty
whose reward sits in escrow, that signature is required, and the prize is
claimed to that same wallet. You can also submit from the **Enter** form
on the bounty page by pasting the repository link and commit and uploading
the bundle. Either way, the commit is snapshotted at submission: later
pushes do not change the entry, so submit the commit you actually checked.

## Step 6: Read your status and fix rejections

```sh
node cli/makefun.mjs status
```

shows your entries and where each stands: submitted, checked, scored, or
rejected. A rejection lists every failed check with its fix. That list is
a gift: apply the fixes, re-bundle if the transcripts changed, re-check
locally, and submit again. You can keep resubmitting until the deadline
within the bounty's daily limit, and your latest entry before the deadline
is the one that counts unless you pick an earlier one.

Two status facts first-timers miss:

- **A rejection is not a verdict on your work.** Most first rejections
  are format misses: a wrong file name, a missing badge line, a session
  that started too early. Fix the named check, not your whole approach.
- **The daily limit is real.** The status output shows what is left of
  it. Spend attempts on entries that already pass the local check.

## Step 7: Claim a reward you won

When results post and your entry placed, you get a notification that the
reward is ready. Claim it from your profile, or from the kit with the
claim id from `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person` honestly: `yes` if you are a US person. The reward
pays in USDC on Solana to your own wallet after an automatic sanctions
screen. A tax form is requested only where US law requires one, which for
most winners means only once yearly winnings reach the reporting
threshold. Unclaimed prizes do not wait forever: claim inside the window
the results page states.

## A first week on make.fun

If the loop above feels like a lot, here is a sane pace for week one. It
is written for someone with a few free evenings, not for someone racing
a deadline.

**Day 1 — Settle in.** Create the account through a referral link, link
GitHub and your wallet, and run `login` from any kit so the command line
is connected to your account. Browse the front page without committing
to anything. Read two bounty pages end to end, including their rules,
just to learn how they are written.

**Day 2 — Pick small and finish it.** Choose the simplest open bounty
with a local grade and a deadline at least a day away. Start a fresh
agent session, build the entry, run the local grade, and bundle and
check it even if the grade is mediocre. The goal today is the loop, not
the leaderboard: a submitted entry teaches more than a perfect draft
that never ships.

**Day 3 — Read the verdict.** Check `status`, read every line of the
check output, and fix whatever it names. If the entry was rejected, fix
and resubmit; if it was accepted, study where the grade lost points and
decide whether a revision is worth another attempt before the deadline.

**Days 4–7 — Repeat with intent.** Enter one bounty at a time, slightly
harder than the last. Keep notes on which checks bit you, which prompts
produced the cleanest agent sessions, and how long each stage really
takes you. After three or four entries, the loop stops feeling like
paperwork and starts feeling like a craft: pick well, build cleanly,
check early, submit early.

The common thread: every entry makes the next one cheaper. The account
setup, the kit habits, and the transcript discipline are all one-time
costs. Pay them on a small bounty, not on the one you most want to win.

## Get your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page carries the same code. You earn rewards
when people sign up through it and take part, plus a share of what they
win for a while after they sign up, paid on top so their own reward stays
whole. Your link, the current reward values, and everything you have
earned live on the **Referrals** tab of your profile.

The part worth saying plainly: only real signups count. A signup is
verified by the same checks that pay referral rewards, with at least a
day of review before anything can be claimed. Your own account, accounts
sharing your network, idle accounts that never take part, and bots never
count. The honest way to earn referrals is the boring way: write
something genuinely useful, like a guide that gets a newcomer to their
first entry, and share it where builders already are.

If this guide helped you, signing up through
[my link](https://make.fun/r/0jnbhk19) (code `0jnbhk19`) is the nicest
way to say thanks, and it costs you nothing.

## Mistakes that cost first-timers their entry

- **Building in a stale session.** The session must start after the
  bounty opens. Reusing yesterday's chat window for today's bounty
  wastes the whole build.
- **Submitting the starter unchanged.** The gate credits only lines your
  agent wrote. A copied starter has none.
- **Pasting the answer in.** Code that first appears in a human message
  or a tool result counts against authorship. Let the agent write it.
- **Skipping the local check.** Rejections count toward the daily limit.
  The check is free; the submission is not.
- **Committing secrets.** Keys in a repository refuse the entry and force
  a history rewrite. Keep them out from the first commit.
- **Submitting the wrong commit.** The snapshot is the commit you name.
  Push, verify the commit hash, check that commit, then submit it.
- **Waiting until the last hour.** Deadlines do not move, and the final
  fix-and-resubmit round always takes longer than you think.

## Questions people ask before their first entry

**Does it cost anything?**
Most bounties are free to enter, and winning one needs no payment. The
model calls your agent makes while building are on your own account, and
a bounty with an entry fee says so on its page before you start.

**Is make.fun legitimate?**
It is run by EZO Labs Inc., a Delaware corporation. Rewards lock in an
open-source on-chain escrow when a bounty opens. It is not makefun.ai,
not the makefun Python library, and not the old Make Fun launchpad on
Base: similar names, different things.

**Do I need to know how to code?**
It helps a lot. Your agent writes the code, but you steer: you pick the
bounty, read the rules, judge the local grade, read the check output, and
decide when an entry is ready. The steering is the skill.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code,
opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by
the kit on their own. Other agents can hand over a session file with
`bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to verify your agent built the entry. The kit strips
credentials, email addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
The transcripts are shown only to you and the organisers, never to other
entrants.

**Can I enter as a team?**
One account per person, and a team enters under one account and splits
any prize itself. The account that submits is the account that claims.

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for builders meeting make.fun for the first time. New here? Sign up with my referral link: https://make.fun/r/0jnbhk19 · code <code>0jnbhk19</code></sub>
