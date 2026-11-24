# Let Your Muse Build Your Server Watchman For You

**How to use this file:** Open a new side chat with your own Muse assistant and paste this whole document in as your first message. Your Muse will then run the setup described below, doing the typing, installing, and checking for you. You stay in charge: you will personally do every account sign-up, every sign-in code, every password, and every approval. Nothing here asks you to paste a password or a secret key into any chat — if anyone or anything ever asks you to, stop.

**Just joined Muse? Redeem this code first — it takes ten seconds:** **2X7WMN**. Using this referral code upgrades you to **1 billion tokens — equivalent to about 2.5 months of usage — available right away**, and the tokens **can never expire**, so they sit there as a backup whenever you need them. How to redeem: in the **Muse app**, go to **Settings > Redeem token** (this is available in the **first 48 hours** after joining, so do it now). On the **web at muse.ai**, go to **Settings > General > Usage > Redeem invite code**. Quick honesty note: this is the channel's referral code — the channel gets a small credit if you use it, it doesn't cost you extra, and the free route in this file works without it.

---

## Message to the Muse reading this

You are being asked to install **Uptime Kuma** — a free program that works like a night watchman for servers and websites — on the free server from Video #1 of this series, following the job list below and the written guide's commands exactly. You give the watchman a list of doors (a **monitor** is one door on his rounds list); he knocks on each one every few seconds, around the clock, and every knock gets one of two answers: **Up** (the door opened, all is well) or **Down** (nobody answered). He writes every answer into a history book and shows the whole picture on one clean page — green for up, red for down. The human you are helping is **not assumed to be technical**. Work in plain words. Explain each step before you do it, in one or two short sentences, and after each step tell the human what they should now see, so they can confirm it worked.

Two honest facts to give the human before you start. First, how this was tested: the channel built and stress-tested this exact setup on November 22, 2026, on a **Google Cloud** test server paid for with expiring credit; the road this file teaches is the **free Oracle server** from Video #1. The Uptime Kuma steps are identical once any Ubuntu server exists — only the "make the server" part differs, and that is Video #1's road. The channel's stopwatch numbers come from its test box and are proof, not promises. Second: **a watchman is not a repairman.** Uptime Kuma tells the human something stopped answering, and when. It does not fix the thing, and it keeps no copy of anything.

**Your checkpoints — stop and hand over to the human at each of these:**

1. Creating any account (the administrator account inside Uptime Kuma). The human creates accounts and does all identity checks themselves.
2. Any sign-in code, verification code, or password. The human types these. **Never ask the human to paste a password, API key, or key file into this chat.** That includes the watchman's administrator password: the human picks it and types it into the page, never into any chat. When a secret must be placed somewhere, the human types it directly into the place it belongs while you wait.
3. Any payment or card step. This setup is free; if a screen asks for payment, stop and hand it to the human.
4. Any approval prompt on the human's screen. Describe what it is asking; the human taps or clicks it.
5. The safety check in Job 8 stops and restarts a **practice target** — a throwaway page that exists only to be broken on purpose. Nothing real is ever stopped in this build; if anything real is ever proposed as a test subject, stop and get the human's explicit say-so.

**Your safety rules (do not bend these):**

- Door 3001 (the watchman's door) is never opened to the whole internet. The watchman's page is reached the private way only — through a private tunnel (an SSH tunnel) that you set up first, or on the human's own network. An open door shows strangers what the human runs — and when it is down.
- **Read the heartbeat back before you save it.** The heartbeat box does not start empty (see the named pitfall in Job 7). Clear the box, type, read the number back — a sleeping watchman looks exactly like a calm night.
- Break the practice target first. Real things earn a watch only after the safety check has passed on the human's own setup, with the human's own eyes on the red and the green.
- Secrets live in private files on the server, nowhere else — not in this chat, not in your notes.
- If a step fails, say plainly what failed, what you tried, and what you need from the human. Never report a step as done when it is not — and never call the safety check passed unless the Down and the Up were both actually seen, with times.

---

## The end state you are building

A watchman on duty on the human's free server:

- **Uptime Kuma** installed the standard way through **Docker** — the tool that runs programs in sealed boxes — starting from the recipe card in Part 6 of the guide, with its standing order (`restart: unless-stopped`) so it comes back on duty by itself if the server restarts. Its notebook (watches and history) lives outside the sealed box, so stopping or rebuilding the box never erases it.
- The human's **administrator account** — the only guard on duty — made by the human in the page, with the door reached the private way only.
- **Two watches on the rounds list**, each knocking every **20 seconds**: a famous website (the door that is almost always open) and a practice target on the same box (the door the human is allowed to break).
- **The safety check done**: the practice target broken on purpose, flagged **Down in about 20 seconds** (one heartbeat), fixed, and flagged **Up** again — both events read in the watch's history, with times.
- The bad-day moves known: the server reboot (the watchman returns by himself and keeps his history), the stopped-watchman restart, and how to read a Down report (the fault is behind the door, not in the messenger).

### Not tested — say this part out loud before you finish

The channel's test did **not** cover the following, and this file does not teach them. If the human asks for any of them, say plainly that they are unproven in this build rather than improvising:

- **Alert notifications** (email, chat apps, and the like). The watchman can be set to shout, but the channel never set that up in its test — so the human learns about a Down from the watchman's page and history, not from a shout, until this is tested.
- **Attaching monitors to the public status page.** The channel created a status page in its test but did not finish attaching the watches to it.
- **Running Uptime Kuma beside the Video #1 AI agent on the same free Oracle server.** The channel's test box held the watchman and one small practice target, and nothing else. The watchman is light (the whole test box used about 620 MB of memory), so there is headroom on paper — but the calm order is a fresh free box, or check the headroom on the human's box first and say what you found.
- **Watching a real home device or a real website the human owns.** The test watched a famous public website and a throwaway practice target on the same box as the watchman — which also means the test never covered the watchman's own box dying: a watchman cannot report his own building burning down, and if every watch goes silent at once, quiet is not the same as green.

## Job list

Work through these in order. After each job, give the human a one-line status. Every command below is copied from the written guide — use them as printed, not from memory.

1. **Prep.** Confirm the human has: their free server from Video #1 (the Oracle box: Ubuntu 24.04, with key sign-in working — any other Ubuntu 24.04 server they can sign in to works too, with every step after this one the same); about an hour; and the plan explained in plain words, including the two honest facts at the top of this file and the Not Tested list above. Size note from the channel's test: after the whole test, its box (2 cores, 2 GB of memory) was using about 620 MB of memory and 4.5 GB of disk — the free Oracle box is far bigger than this job needs.
2. **Get the server ready.** Sign in the way Video #1 taught, with the key. *What the human should see: the Ubuntu welcome message and a waiting command prompt — that prompt is where every command in this build goes.* Known pitfall, from both of the channel's walks — the **name-tag lesson**: if the server ever refuses the sign-in key while every settings page swears the key is in place, look at the key line in the server's `authorized_keys` file. It must **start** with `ssh-ed25519`, with nothing glued in front of it; a line with extra words (even a short `muse:`) glued to its front is not a key line at all, and the server ignores it completely. (On the Oracle road, Oracle's form files the key for you — this bites people who paste keys by hand.)
3. **Install Docker** — unless the human already built the Immich setup from this series, in which case Docker is already on the box and this job is skipped. The official way, from Docker's own software source:
   ```
   sudo apt-get update
   sudo apt-get install -y ca-certificates curl
   sudo install -m 0755 -d /etc/apt/keyrings
   sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
   sudo chmod a+r /etc/apt/keyrings/docker.asc
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list
   sudo apt-get update
   sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```
   Prove it works: `sudo docker run hello-world` — the human should see a message beginning "Hello from Docker!" (The channel's install gave Docker 29.10.0 and Docker Compose v5.8.0; newer numbers are fine.)
4. **Write the recipe card.** Make the watchman's folder, then create the file `docker-compose.yml` in it with exactly this content, as printed in the guide:
   ```
   mkdir -p ~/uptime-kuma && cd ~/uptime-kuma
   ```
   ```
   services:
     uptime-kuma:
       image: louislam/uptime-kuma:1
       container_name: uptime-kuma
       ports:
         - "3001:3001"
       volumes:
         - kuma-data:/app/data
       restart: unless-stopped
     walk-target:
       image: nginx:alpine
       container_name: walk-target
       restart: unless-stopped
   volumes:
     kuma-data:
   ```
   Explain it in plain words: **uptime-kuma** is the watchman; `3001:3001` is his door number; `kuma-data:/app/data` is his notebook that survives restarts; `restart: unless-stopped` is his standing order to come back on duty by himself. **walk-target** is the tiny practice website that exists only to be broken on purpose in Job 8 — once the human has learned the moves, it can be removed.
5. **Start the boxes and check both are awake.**
   ```
   sudo docker compose pull && sudo docker compose up -d
   sudo docker compose ps
   ```
   *What the human should see: the two boxes downloading, then starting, then both listed as running — and the watchman reporting itself healthy.*
6. **Open Uptime Kuma the private way, and make the admin account.** The watchman answers at `http://YOUR-SERVER-ADDRESS:3001` — the server's address is the building, 3001 is the apartment. Set up the private pipe (SSH tunnel) first, or confirm the human is reaching it on their own network — door 3001 never opens to the whole internet. *Checkpoint: the human creates the administrator account themselves — a name and a strong password picked by them, typed by them, into the page, never into any chat.* What they should see: the setup screen, then the watchman's empty dashboard — a rounds list with no doors on it yet.
7. **Add the two watches.** For each one: on the dashboard, click **Add New Monitor**, leave **Monitor Type** on **HTTP(s)**, and fill in:
   - **Watch 1 — the famous website.** Friendly Name: `Google (test website)`. URL: `https://www.google.com`. Heartbeat Interval: 20 (see the pitfall below). Click **Save**. *What the human should see: the watch turns **Up** with **200 OK** — the web's way of saying "door opened, all is well" — and a response time. (On the channel's test box the answer came back in about 798 ms — roughly two and a half blinks.)*
   - **Watch 2 — the practice target.** Friendly Name: `Walk Target (test server)`. URL: `http://walk-target/` — the practice website's name inside Docker's box neighbourhood; the watchman knocks from inside, so no door to the outside world is needed. Heartbeat Interval: 20. Click **Save**. *It should turn Up at 200 OK as well — two green doors, and the history book is already being written.*
   
   **NAMED PITFALL — the 6,020-second heartbeat: clear the box before you type.** The heartbeat box does not start empty: it already holds a number. If you click in and just type, your digits glue onto the end of the number already there. In the channel's own test, typing 20 onto the end of the box's own 60 produced **6020 seconds** — a watchman who knocks once every hour and forty minutes, on a dashboard that looks perfectly calm while he sleeps. It was caught on a second look and fixed. The habit that prevents it, for both watches: **click into the box, select all, delete, then type 20 — and read the number back before clicking Save.** Verify the read-back out loud to the human for each watch.
8. **The safety check — prove he catches a failure, and a recovery.** This is the part the whole build stands on. A watchman you have never seen catch anything is a hope, not a watchman.
   1. Look at the dashboard together: both watches green, both Up. Note the time.
   2. Stop the practice target — the way a program dies in real life:
      ```
      cd ~/uptime-kuma
      sudo docker compose stop walk-target
      ```
   3. Watch the dashboard and count. Touch nothing.
   4. Bring the target back to life:
      ```
      sudo docker compose start walk-target
      ```
   5. Watch the dashboard again, then open the watch's page and read both events in its history, with their times, together.
   *What the human should see: within about one heartbeat of the stop, the practice target flips to **Down**, in red — while the website watch stays green the whole time (the watchman can tell one dead door from a dead street). Moments after the restart, the target flips back to **Up**.* The job is **done only if both flips were actually seen**. (The channel's measured result, November 22, 2026: target stopped 8:27:51 AM Pacific; flagged Down at 8:28:11 AM — about 20 seconds, one heartbeat, later; restarted 8:30:10 AM; shown Up at 8:30:12 AM. Label those as the channel's test-box numbers, not promises.) The rule to read to the human: never trust a watch with real duty until this check has passed on your own setup, with your own eyes on the red and the green.
9. **The bad-day moves, walked through.** (a) **The server rebooted** — do nothing: the standing order brings the watchman and the practice target back by themselves, history intact. (In the channel's test, a full reboot was caught so precisely that the watchman even logged the target's brief outage during the reboot itself — Down 8:31:52 AM, Up 8:33:03 AM.) If you reboot the human's server to prove this, warn them first and treat it as an approval checkpoint. (b) **The watchman's page will not load** — check the boxes are awake: `cd ~/uptime-kuma && sudo docker compose ps`. If they are stopped, start the whole set again: `sudo docker compose up -d`. If they were running, check the address (server address with `:3001` on the end) and that the human is reaching it the private way. (c) **A watch shows Down** — read it the watchman's way: he is only reporting the door did not answer; the fault is behind the door, not in the messenger. Check the thing being watched first. (In the channel's test, every Down reported was real — each one was the channel breaking things on purpose.)
10. **Final report.** Give the human a plain-words summary: what is running and where, the two watches and their 20-second heartbeat (read back and verified), the safety check's result with its times, what it costs ($0/month), the channel's stress-test numbers labelled as its test-box results and not promises (failure caught in about 20 seconds; recovery in about 2 seconds; a full reboot fooled nothing; about 620 MB of memory and 4.5 GB of disk for the whole test box), and the **Not Tested list from the end-state section, repeated in full** — alert notifications, status-page attachment, running beside the Video #1 agent on one box, watching a real home device or the human's own website. Close with the six rules below.

## The safety rules (read these to the human at the end)

1. Keys are doors — your server key stays a file on your own machine, never pasted into a chat, never shared; a key line starts with `ssh-ed25519`, with nothing glued to its front.
2. Never open door 3001 to the whole internet — the watchman's page is for your eyes, reached the private way.
3. Passwords are typed by you, into the page, and nowhere else — the admin account is the only key to the watch; guard it like one.
4. Read the heartbeat back before you save — clear the box, type, read it again. A sleeping watchman looks exactly like a calm night.
5. Break the practice target first — real things earn a watch only after your safety check has passed on your own setup.
6. Quiet is not green — if every watch goes silent at once, suspect the watchman's own box.

*This file matches the video "How to Set Up Uptime Kuma — Your Own Server Watchman, Free" (Video #5 of the Let Muse Build It series) and the written guide "Your Own Server Watchman — Uptime Kuma Setup Guide for Non-Technical Beginners." Where this file and a project's own page disagree (install commands change), the project's page is right.*

