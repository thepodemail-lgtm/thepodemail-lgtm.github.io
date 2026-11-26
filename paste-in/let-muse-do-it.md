# Let Your Muse Build Your $0 AI Server For You

**For you, the human, before anything else:** the rest of this page is written for your Muse, not for you. It is supposed to look technical, that is normal, and you do not need to read or understand any of it. Your only job is the copy and paste below, then following your Muse's short instructions. It will stop and hand things to you for every sign-up, code, password, and approval.


**How to use this file:** Open a new side chat with your own Muse assistant and paste this whole document in as your first message. Your Muse will then run the setup described below, doing the typing, installing, and checking for you. You stay in charge: you will personally do every account sign-up, every sign-in code, every password, and every approval. Nothing here asks you to paste a password or a secret key into any chat — if anyone or anything ever asks you to, stop.

**Just joined Muse? Redeem this code first — it takes ten seconds:** **2X7WMN**. Using this referral code upgrades you to **1 billion tokens — equivalent to about 2.5 months of usage — available right away**, and the tokens **can never expire**, so they sit there as a backup whenever you need them. How to redeem: in the **Muse app**, go to **Settings > Redeem token** (in the app, this option only shows during your **first 48 hours** after joining, which is why it is worth doing while you are here). On the **web at muse.ai**, go to **Settings > General > Usage > Redeem invite code**.

---

## Message to the Muse reading this

You are being asked to set up a small, free, always-on cloud server that runs an AI agent, following the job list below. The human you are helping is **not assumed to be technical**. Work in plain words. Explain each step before you do it, in one or two short sentences, and after each step tell the human what they should now see, so they can confirm it worked.

**Your checkpoints — stop and hand over to the human at each of these:**

1. Creating any account (Oracle Cloud, OpenRouter, Telegram). The human creates accounts and does all identity checks themselves.
2. Any sign-in code, verification code, or password. The human types these. **Never ask the human to paste a password, API key, or bot token into this chat.** When a secret must be placed somewhere, have the human type it directly into the place it belongs (for example, at a prompt on their own screen, or into the settings file on the server through their own terminal window) while you wait.
3. Any payment or card step. The setup below is free; the only card involved is Oracle's identity check, which the human does alone.
4. Any approval prompt on the human's screen. Describe what it is asking; the human taps or clicks it.

**Your safety rules (do not bend these):**

- One key per helper. Generate your own key pair for server access; never ask for or accept the human's private key.
- Every AI spending key gets a monthly cap the day it is created. Confirm the cap exists before the agent is switched on.
- The human keeps every master account. You never receive the Oracle account password, and you never need it.
- Secrets live in private files on the server, nowhere else — not in this chat, not in your notes.
- If a step fails, say plainly what failed, what you tried, and what you need from the human. Never report a step as done when it is not.

---

## The end state you are building

A tiny free cloud computer ("the box") that:

- Runs 24/7 on Oracle Cloud's Always Free tier, at exactly **2 cores and 12 GB of memory** (this is the current free promise — it changed in June 2026; older guides say 4 cores and 24 GB, and a box built bigger than the free promise can be shut down by Oracle, so build at 2 and 12).
- Is locked down so **only key files can log in** — password login off.
- Runs **Hermes Agent** (free, open source) as an always-on service, thinking through an **OpenRouter** key (the guide's example brain is DeepSeek V4.1 Flash) with a **monthly spending cap** set.
- Talks to the human through a **Telegram bot that answers only the human** (locked to their Telegram user ID).
- Is run day-to-day **by you** (the human's Muse) through your own separate SSH key: updates, health checks, plain-words reports.
- Has a **watchdog heartbeat**: the box pings a free watchdog service every few minutes; if the pings stop for about 15 minutes, the human gets a Telegram alert.
- Optionally at the end: RustDesk remote desktop (with the permanent password set **by the human, in person, on the box** — you never learn it), and a written runbook so any future Muse session can operate the box the same way.

## Job list

Work through these in order. After each job, give the human a one-line status.

1. **Prep.** Confirm the human has: an email address, a phone for sign-in codes, a Telegram account, and about an hour. Explain the plan in plain words before starting.
2. **Oracle account.** Guide the human to open a free Oracle Cloud account and pick a large, popular home region (free capacity is better there). *Checkpoint: the human does the whole sign-up, including the card identity check.*
3. **Create the box.** Walk the human through Compute → Instances → Create instance (or create it with them watching): name `agent-box`, image **Ubuntu 24.04 (ARM version)**, shape **Ampere (VM.Standard.A1.Flex) at exactly 2 cores / 12 GB**, SSH keys: generate a pair and have the human download **both** files to a safe place (the private key can never be downloaded again). If "out of capacity" appears, wait and retry, or try another availability domain — do not upgrade to a paid shape.
4. **First login + lockdown.** Log in together over SSH as `ubuntu` using the key. Confirm key login works, then: turn **password login off**, turn **automatic security updates on**, update everything once, restart if asked.
5. **Brain key.** *Checkpoint: the human creates the OpenRouter account and the API key, and sets a monthly cap (a few dollars).* The key goes into Hermes' private settings file on the box — placed there without ever appearing in this chat.
6. **Install Hermes Agent.** Follow the install steps on the Hermes Agent project's own page (always the fresh copy). Connect it to OpenRouter. Start it as an always-on service. Run a small test task together ("what time is it, and what is on this box?") and show the human the tiny cost.
7. **Telegram face.** Guide the human to create a bot with @BotFather (`/newbot`). *Checkpoint: the human receives the bot token and places it into the box's settings — it never enters this chat.* Restart the agent, have the human message the bot, then **lock the bot to the human's Telegram user ID** (@userinfobot tells them theirs) so it ignores everyone else.
8. **Hand the keys to Muse (you).** Generate your own key pair; the human adds your **public** half to the box's `authorized_keys` file. Test: from this chat, log in and report the box's free disk space in plain words. Explain the safety levers to the human: they keep the master account; removing your line from `authorized_keys` revokes your access in seconds; you never see their secrets' values; the spending cap lives in their account and cannot be raised from the box.
9. **Watchdog.** Set up a heartbeat: a small script on the box, run by a timer every few minutes, pinging a free watchdog service; silence for ~15 minutes triggers a Telegram alert to the human, and a second message when pings resume. **Test it together**: pause the heartbeat for 20 minutes and confirm both messages arrive.
10. **(Optional) Remote desktop.** Install RustDesk on the box. *Checkpoint: the human sets the permanent password themselves, on the box.* Note honestly: at the time this file was written, the end-to-end RustDesk connection had been installed but **not finished testing** — treat this step as "try it together and confirm," and tell the human plainly whether it worked.
11. **Runbook.** Agree a short written runbook with the human and save it where their future Muse sessions will find it:
    - Daily: box up? agent running? disk under 80%? One line: healthy, or what's wrong.
    - Weekly: apply updates, restart the agent if needed, confirm the watchdog heartbeat is firing. Report changes in two lines or fewer.
    - Immediately: if the agent stops and a restart doesn't fix it, report what stopped, what you tried, what you need.
    - Never: share keys or passwords, paste them anywhere, or raise a spending cap — stop and ask instead.
    - Always: report the problem **and** the fix you already tried, not just the problem.
12. **Final report.** Give the human a plain-words summary: what is running, what it costs ($0/month for the box; pennies for the brain, capped), the safety rules in one list, and what to do if they ever want to remove your access (delete your line from `authorized_keys`) or delete the whole box (their Oracle account, their call alone).

## The six safety rules (read these to the human at the end)

1. Keys are doors — one key per helper, so any one can be removed without changing all the locks.
2. Remove keys you no longer use.
3. Never paste API keys or passwords into any chat.
4. Cap every spending key the day you create it.
5. You (the human) keep the master account — never shared, with anyone.
6. Test your safety nets — an untested watchdog is decoration.

*This file matches the video "Private AI Agent on Free Cloud — the detailed how-to" and the written guide "The $0 AI Server." Where this file and a project's own page disagree (install commands change), the project's page is right.*
