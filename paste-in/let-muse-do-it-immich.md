# Let Your Muse Build Your Private Photo Vault For You

**For you, the human, before anything else:** the rest of this page is written for your Muse, not for you. It is supposed to look technical, that is normal, and you do not need to read or understand any of it. Your only job is the copy and paste below, then following your Muse's short instructions. It will stop and hand things to you for every sign-up, code, password, and approval.


**How to use this file:** Open a new side chat with your own Muse assistant and paste this whole document in as your first message. Your Muse will then run the setup described below, doing the typing, installing, and checking for you. You stay in charge: you will personally do every account sign-up, every sign-in code, every password, and every approval. Nothing here asks you to paste a password or a secret key into any chat — if anyone or anything ever asks you to, stop.

**Just joined Muse? Redeem this code first — it takes ten seconds:** **2X7WMN**. Using this referral code upgrades you to **1 billion tokens — equivalent to about 2.5 months of usage — available right away**, and the tokens **can never expire**, so they sit there as a backup whenever you need them. How to redeem: in the **Muse app**, go to **Settings > Redeem token** (this is available in the **first 48 hours** after joining, so do it now). On the **web at muse.ai**, go to **Settings > General > Usage > Redeem invite code**. Quick honesty note: this is the channel's referral code — the channel gets a small credit if you use it, it doesn't cost you extra, and the free route in this file works without it.

---

## Message to the Muse reading this

You are being asked to install **Immich** — a free program that gives the human their own private Google Photos: a timeline, face recognition, search, albums, and a phone app that backs up the camera roll by itself — on the free Oracle server from Video #1 of this series, following the job list below and the written guide's commands exactly. The difference from Google Photos is where the photos live: on a server the human controls, as real files, at full original quality. The human you are helping is **not assumed to be technical**. Work in plain words. Explain each step before you do it, in one or two short sentences, and after each step tell the human what they should now see, so they can confirm it worked.

Two honest facts to give the human before you start, because the guide states them plainly. First, how this was tested: the channel built and stress-tested this exact setup on November 18, 2026, on a **Google Cloud** test server paid for with expiring credit; the road this file teaches is the **free Oracle server** from Video #1. The Immich steps are identical once any Ubuntu server exists — only the "make the server" part differs, and that is Video #1's road. The channel's stopwatch numbers come from its test box and are proof, not promises. Second: **one copy is not a backup.** This build proves Immich keeps originals whole and hands them back. It does not make a second copy of the library anywhere else — a full backup of the server itself was **not part of the channel's test walk** and is not taught here. Until the human has another copy somewhere, their originals stay on their phone or computer as well.

**Your checkpoints — stop and hand over to the human at each of these:**

1. Creating any account (the administrator account inside Immich; family members' accounts). The human creates accounts and does all identity checks themselves.
2. Any sign-in code, verification code, or password. The human types these. **Never ask the human to paste a password, API key, or key file into this chat.** That includes the database password in Job 5: the human picks it and it is placed into the settings file without ever appearing in this chat. When a secret must be placed somewhere, the human types it directly into the place it belongs while you wait.
3. Any payment or card step. This setup is free; if a screen asks for payment, stop and hand it to the human.
4. Any approval prompt on the human's screen. Describe what it is asking; the human taps or clicks it.
5. Deleting anything. The safety check in Job 9 deletes the human's **computer copy of a throwaway test photo** — copies they can afford to lose, chosen by the human. Nothing real gets deleted anywhere in this build without the human's explicit say-so, and real photos are never the test material.

**Your safety rules (do not bend these):**

- Door 2283 (Immich's door) is never opened to the whole internet. Immich is reached the private way only: on the home network, or through a private tunnel (an SSH tunnel) that you set up first. Set that pipe up **before** a single real photo is uploaded.
- Test with throwaway photos first. Real photos move in only after the safety check has passed on the human's own setup, with the human's own eyes on the fingerprints.
- One copy is not a backup (see above). Never tell the human their photos are "backed up" in the full sense — say what is true: Immich holds a whole, proven copy, and their originals should also stay where they were.
- Secrets live in private files on the server, nowhere else — not in this chat, not in your notes.
- If a step fails, say plainly what failed, what you tried, and what you need from the human. Never report a step as done when it is not — and never call the safety check passed unless the two fingerprints were actually compared.

---

## The end state you are building

The human's own private photo library, on their free server:

- **Immich** running on the free Oracle server from Video #1 (Ubuntu 24.04), installed the official way through **Docker** — the tool that runs programs in sealed boxes. Immich travels as four parts that start together: **immich_server** (the app itself), **immich_machine_learning** (the helper that finds faces and makes the library searchable), **immich_postgres** (the card catalog — the index that remembers which photo is which), and **immich_redis** (the errand runner passing jobs between them). All four running and healthy. (The channel's November 2026 install reported itself as Immich 3.4.1; a newer number is fine.)
- The human's **administrator account**, made by the human in the page, and — if they want them — **sealed accounts for family**: each person's library starts empty and stays sealed (in the channel's test, a second account saw zero photos, and even a direct link to the first account's photo was refused).
- The **phone app backing up** the camera roll as full originals, over the private route only.
- **The safety check passed**: a throwaway photo deleted on the human's side, downloaded back from Immich, and proven **byte-for-byte identical** by matching fingerprints (`sha256sum`) — before any real photo is trusted to it.
- The bad-day moves known: Trash restore inside Immich, Download to get an original out, the full restart, and the server reboot that Immich survives by itself.

## Job list

Work through these in order. After each job, give the human a one-line status. Every command below is copied from the written guide — use them as printed, not from memory.

1. **Prep.** Confirm the human has: their free Oracle server from Video #1 (Ubuntu 24.04, 2 cores, 12 GB of memory) with key sign-in working; about an hour; a phone or computer for photos; and **a few throwaway photos — copies they can afford to lose** — for the first upload and the safety check. Explain the honest facts at the top of this file before starting. One more honest note: the channel's test box was a clean server with nothing else on it. If the human's free box already runs the Video #1 agent, the two were **not tested** side by side — there is headroom on paper (Immich's busiest moment used about 4 GB of the test box's 8 GB; the free box has 12 GB), but the calm order is a fresh free box, or check the memory headroom first and say what you found.
2. **Get the server ready.** Sign in the way Video #1 taught, with the key. *What the human should see: the Ubuntu welcome message and a waiting command prompt — that prompt is where every command in this build goes.*
3. **Install Docker.** The official way, from Docker's own software source — not the older copy in Ubuntu's cupboard:
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
   Prove it works: `sudo docker run hello-world` — the human should see a message beginning "Hello from Docker!" (The channel's install took about 90 seconds and gave Docker 29.10.0 and Docker Compose v5.8.0; newer numbers are fine.)
4. **Download Immich's two official files** — the recipe card and the settings card — straight from the Immich project, into their own folder:
   ```
   mkdir -p ~/immich && cd ~/immich
   wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
   wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env
   ```
   Explain the two files in plain words: `docker-compose.yml` lists Immich's four parts and how they connect (the human never edits it); `.env` is the settings card — where the photos live (a folder called `library`), where the card catalog lives (a folder called `postgres`), and the database password. Exactly two things on it get edited, in the next job.
5. **Set the database password and timezone.** *Checkpoint: the human picks the database password — their own, **letters and numbers only, no spaces and no symbols** (that rule comes from the settings file itself), never reused from anywhere else — and it goes into the settings file without ever appearing in this chat.* The guide's commands, with the human's own password and timezone in place of the examples:
   ```
   sed -i "s/^DB_PASSWORD=.*/DB_PASSWORD=YOUR-OWN-PASSWORD/" .env
   echo "TZ=America/Los_Angeles" >> .env
   ```
   Both commands print nothing when they work — silence is success here.
6. **Start Immich and check all four parts.**
   ```
   sudo docker compose pull && sudo docker compose up -d
   sudo docker compose ps
   ```
   *What the human should see: the four parts downloading, then starting (about 3 minutes on the channel's test box), then listed as running and, a moment later, healthy.* Known pitfall, from the channel's own walk — the **name-tag lesson**: if the server ever refuses the sign-in key while every settings page swears the key is in place, look at the key line in the server's `authorized_keys` file. It must **start** with `ssh-ed25519`, with nothing glued in front of it. A line with a short `name:` glued to its front is not a key line at all, and the server ignores it completely. (On the Oracle road, Oracle's form files the key for you — this bites people who paste keys by hand.)
7. **Open Immich the private way, and make the first account.** Immich answers at the server's address with its door number: `http://YOUR-SERVER-ADDRESS:2283`. Before opening it, set up the private pipe (SSH tunnel) or confirm the human is reaching it on their own network — door 2283 never opens to the whole internet, and the pipe goes in **before** any real photo is uploaded. *Checkpoint: the human creates the administrator account themselves — their name, email, and a strong password typed by them, into the page, never into any chat.* What they should see: a welcome screen asking for the administrator account, then their empty library.
8. **Upload the test photos.** From the phone: install the free Immich app, type the same server address (with `:2283` on the end), sign in, turn on **Backup**, and choose which photo folders it backs up. From a computer: open the address, sign in, click **Upload**, pick the files. **Throwaway photos only in this job.** Then set expectations: the helper studies each new photo (thumbnails, faces, search) as background jobs — after a big upload this takes a while and is normal, not a fault. (In the channel's test, the background work for 225 photos finished in about five minutes with not one job failing.) If the human wants family accounts, add them now, as administrator, under Administration → Users — each new library starts empty and sealed.
9. **The safety check — the job this whole build stands on.** With one throwaway photo:
   1. On the computer, take the photo's **fingerprint** — a long string that identifies the file exactly; if two fingerprints match letter for letter, the files are the same file, bit for bit: `sha256sum testphoto.jpg`. Write the fingerprint down.
   2. Upload that photo to Immich (Job 8) and wait until it appears in the library.
   3. *Checkpoint: the human confirms this is the throwaway photo, then deletes their computer's copy* — the way the photo would be gone if the computer died.
   4. In Immich, open the photo and choose **Download**. A file comes back.
   5. Fingerprint the returned file the same way, and compare, letter for letter, in front of the human.
   The job is **done only if the two fingerprints match exactly**. (The channel ran exactly this check on November 18, 2026, with two photos — both came back byte-for-byte identical — and again after a full stop-and-start and after a complete server reboot, with every spot-checked file still matching.) If the fingerprints do not match, stop: do not move any real photo, and say plainly what happened. The rule to read to the human: never delete the only copy of a real photo until this check has passed on your own setup, with your own eyes on the fingerprints.
10. **The bad-day moves, tried once each on test photos.** (a) Delete a photo inside Immich — it goes to **Trash**, not oblivion; open Trash, pick it, choose **Restore**. (b) Restart the whole set the way an owner would for an update:
    ```
    cd ~/immich
    sudo docker compose down
    sudo docker compose up -d
    ```
    (In the channel's test, Immich was answering again 25 seconds after the restart began, library count unchanged.) (c) Note, without necessarily doing it today: after a full server reboot, Immich starts by itself — in the channel's test all four parts were back within about 35 seconds, library exactly as before.
11. **Final report.** Give the human a plain-words summary: what is running (the four parts, all healthy), where their photos live, the safety check's result with the fingerprints that proved it, what it costs ($0/month), the channel's stress-test numbers labelled as its test-box results and not promises (220 photos uploaded in 34 seconds with zero errors; one 622 MB video in 13 seconds; every background job drained with zero failures), and the honest limits that remain: one copy is not a backup — a full server backup was not part of the channel's walk and is not taught here, so originals stay on the phone or computer too; moving an existing Google Photos library into Immich in bulk is **not tested**; reaching Immich from outside the home is **not tested**; Immich has none of Google Photos' social side (no public pages, no automatic movies) in what was tested. Close with the six rules below.

## The safety rules (read these to the human at the end)

1. Keys are doors — your server key stays a file on your own machine, never pasted into a chat, never shared; a key line starts with `ssh-ed25519` and has nothing glued to its front.
2. Never open door 2283 to the whole internet — Immich is for your own devices, reached the private way.
3. Passwords are typed by you, into the page, and nowhere else — including the database password: your own, letters and numbers only, used for nothing else.
4. Test with throwaway photos first — real photos move in only after your safety check has passed.
5. One copy is not a backup — keep another copy of anything precious until you have a backup routine.
6. Test your safety nets — the restore check, the Trash restore, the restart. A safety net you have never tested is decoration.

*This file matches the video "How to Set Up Immich — Your Own Private Google Photos" (Video #4 of the Let Muse Build It series) and the written guide "Your Own Private Google Photos — Immich Setup Guide for Non-Technical Beginners." Where this file and a project's own page disagree (install commands change), the project's page is right.*

