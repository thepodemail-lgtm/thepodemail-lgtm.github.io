# Let Your Muse Build Your Server Watchdog For You

**How to use this file:** Open a new side chat with your own Muse assistant and paste this whole document in as your first message. Your Muse will then run the setup described below, doing the typing, installing, and checking for you. You stay in charge: you will personally do every account sign-up, every sign-in code, every password, and every approval. Nothing here asks you to paste a password or a secret key into any chat — if anyone or anything ever asks you to, stop.

**Just joined Muse? Redeem this code first — it takes ten seconds:** **2X7WMN**. Using this referral code upgrades you to **1 billion tokens — equivalent to about 2.5 months of usage — available right away**, and the tokens **can never expire**, so they sit there as a backup whenever you need them. How to redeem: in the **Muse app**, go to **Settings > Redeem token** (this is available in the **first 48 hours** after joining, so do it now). On the **web at muse.ai**, go to **Settings > General > Usage > Redeem invite code**. Quick honesty note: this is the channel's referral code — the channel gets a small credit if you use it, it doesn't cost you extra, and the free route in this file works without it.

---

## Message to the Muse reading this

You are being asked to add a watchdog to the small free cloud server the human built in Video #1 of this series — the box that runs their AI agent ("the helper"). The watchdog has two layers: an outside watcher that notices if the whole box goes silent, and a checker on the box that restarts the helper if it stops or gets stuck. The human you are helping is **not assumed to be technical**. Work in plain words. Explain each step before you do it, in one or two short sentences, and after each step tell the human what they should now see, so they can confirm it worked.

This build starts where Video #1 ended. If the human does not yet have the Video #1 server running, stop and say so plainly — this file does not build that server; the Video #1 instruction file does.

**Your checkpoints — stop and hand over to the human at each of these:**

1. Creating any account (a free watchdog service account, if that route is chosen; Telegram, if they do not have it yet). The human creates accounts and does all identity checks themselves.
2. Any sign-in code, verification code, or password. The human types these. **Never ask the human to paste a password, API key, or token into this chat.** When a secret must be placed somewhere, have the human type it directly into the place it belongs while you wait.
3. Any payment or card step. This setup is free; if any screen asks for a card or a payment, stop and hand it to the human.
4. Any approval prompt on the human's screen. Describe what it is asking; the human taps or clicks it.
5. The live test in the job list involves pausing the heartbeat and stopping the helper on purpose. Get the human's clear go-ahead before each break, and tell them what will happen and for how long before you do it.

**Your safety rules (do not bend these):**

- The heartbeat carries liveness and nothing else — the box's name and the time. No files, no secrets, no personal data, ever.
- The heartbeat token is a secret. It lives in a private file on the box — never in this chat, never on screen, never in your notes.
- Secrets live in private files on the server, nowhere else.
- One alert per outage, then quiet, and one note when things return. Never build a watcher that spams the human — a muted alarm is no alarm.
- A restarter must know when to stop. If the helper keeps falling over, stop restarting it and alert the human instead. Restart the known; report the strange; never improvise.
- If a step fails, say plainly what failed, what you tried, and what you need from the human. Never report a step as done when it is not — and never report a test as passed when it was not run.

---

## The end state you are building

The Video #1 box, now guarded by a watchdog with two layers:

- **The heartbeat:** a tiny script on the box, run by a timer (the schedule list called cron — the proven route) every **5 minutes**, sending one small message to the watcher: this box, this time, alive.
- **The outside watcher:** living somewhere else — never on the box it watches, because a watcher cannot report its own death. Either a free watchdog service, or a second tiny free box of the human's own. Both do the same job.
- **The silence limit:** **15 minutes** — three missed heartbeats in a row — triggers exactly **one** Telegram alert to the human. When the heartbeats return, exactly **one** "back up" note follows.
- **The restarter:** the helper runs as a service with its restart line switched on, so the box restarts it if it stops. A small checker also peeks every few minutes for the quieter failure — the helper running but stuck — and restarts it **once**, writing one line in a log saying what happened and when.
- **Guardrails:** a restart limit. After it, the checker stops restarting and sends the alert instead — a human needs to look.
- **Tested, not hoped:** the whole thing has been broken on purpose, twice, with the times written down — the silence test and the helper test in the job list below. An untested watchdog is a hope, not a watchdog.

## Job list

Work through these in order. After each job, give the human a one-line status.

1. **Prep.** Confirm the human has: their finished Video #1 server with the helper running, a free Telegram account (alerts land there), and about 45 minutes. Explain the two layers in plain words before starting. If the Video #1 box does not exist yet, stop here and point them to Video #1.
2. **The heartbeat script.** Write the one short line that sends the heartbeat: this box, this time, alive. The two parts that must be filled in are the watcher's address and the secret token. *Checkpoint: the token goes into a private file on the box — the human watches you place it there; it never appears in this chat.*
3. **The timer.** Hand the heartbeat to cron, the box's simple schedule list, so it fires every 5 minutes, day and night. (Honest note to give the human: a newer timer called a systemd timer exists, but this channel has not walked that variant fresh — it is **not tested yet**. Use cron; it is proven.) Checkpoint together: a new heartbeat line should land every 5 minutes, showing nothing but the box's name and the time. If no lines appear, the timer — not the script — is the first suspect.
4. **Pick the watcher.** Explain the two honest choices: **Choice A**, a free watchdog service — someone else's watcher, set up in minutes (real prices from the video, checked November 2026: Healthchecks.io is free for 20 jobs, first bigger plan $20/month; UptimeRobot free for 50 monitors, paid from $12/month billed yearly; Better Stack free for 10 monitors, responder plan $29/month per person). **Choice B**, a second tiny free box of their own — $0/month, more setup, fully theirs. The human picks; the job after this is identical either way. *Checkpoint: if Choice A needs an account, the human creates it.*
5. **Connect the watcher and set the silence limit.** Point the watcher at the heartbeat, with the token matching on both ends. Set the silence limit to 15 minutes (three missed heartbeats). Set the alert rules: exactly one alert per outage, exactly one "back up" note when pings return, both to the human's Telegram. Checkpoint together: the watcher's status page lists the box as UP, with the last heartbeat under 5 minutes old. If it says UNKNOWN, no heartbeat has ever arrived — check the token match first.
6. **Run the helper as a service.** Register the helper as a service with the restart line switched on: if this stops, start it again. Confirm the setting is really in place before moving on.
7. **Add the checker.** Install the small checker that peeks every few minutes and asks two questions: is the helper alive, and is it actually working — did it do anything lately? If not: one restart, and one line in the log with the time, what stopped, and what was done. Add the guardrail from the safety rules: if the helper keeps falling over, the checker stops restarting and alerts instead; if the checker sees something strange — a program running that it did not expect — it writes down what it saw and waits for a human.
8. **Live test one — the silence test.** *Checkpoint: explain the timeline first and get the human's go-ahead.* Pause only the heartbeat — the schedule line, nothing else; the box and the helper keep working. Write down the time. Then wait the full 15-minute silence limit without poking anything. Exactly one "your server is down" alert should arrive on the human's phone. Resume the heartbeat, write down the time, and exactly one "back up" note should follow. (The shape to expect, from this channel's own real test on Nov 13, 2026: heartbeat paused 7:09 AM, one down alert 7:20 AM, heartbeat resumed 7:21 AM, one recovery note 7:25 AM.) Read any other outcome plainly: zero messages means the watcher never noticed — check the token match and the silence limit; a down message but no back-up message usually means the heartbeat resumed under a slightly different name; three or more messages means something is flapping and the one-alert rule is not holding.
9. **Live test two — the helper test.** *Checkpoint: get the human's go-ahead.* Stop the helper on purpose. The checker should restart it — once — and write the restart in the log. Read the log line together: time, what stopped, what was done. If the helper restarts twice, or not at all, the guardrails from Job 7 are where to look. Do not call the watchdog done until both live tests have passed.
10. **Care routine.** Agree a short routine with the human and save it where their future Muse sessions will find it:
    - Monthly: pause the heartbeat for real, like a fire drill, and watch the alert land. Safety systems rot quietly; drills are how you find out.
    - When an alert arrives: read the log line first — time, what stopped, what was done — before touching anything.
    - Never: loosen the one-alert rule, move the watcher onto the box it watches, or let the heartbeat carry anything but liveness.
11. **Final report.** Give the human a plain-words summary: the two layers and where each lives, the silence limit, where alerts land, the results of both live tests with their times written down, what it costs ($0/month on the free routes), and the honest labels that remain — the systemd-timer variant is not tested yet; everything else in this file was walked by the channel before it was written down.

## The safety rules (read these to the human at the end)

1. A heartbeat carries "I'm alive" and nothing else — no secrets, ever.
2. The watcher lives somewhere else — it cannot report its own death.
3. Fifteen minutes of silence; one alert per outage; one note on return.
4. The helper runs as a service; the checker restarts the stuck — once — and logs it.
5. A restarter that keeps failing stops, and asks a human.
6. Secrets live in private files on the server — never in a chat.
7. Test it for real, then test it monthly — a watchdog never tested is a hope, not a watchdog.

*This file matches the video "How to Set Up a Watchdog for Your Server" (Video #2 of the Let Muse Build It series) and the written guide "The $0 AI Server" — that guide's watchdog section (its Part 8 and Going Further material) is the written companion for this build; there is no separate watchdog guide. Where this file and a project's own page disagree (install commands and services change), the project's page is right.*

