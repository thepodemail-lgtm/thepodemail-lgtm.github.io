# Let Your Muse Build Your Whole-House Ad Blocker For You

**For you, the human, before anything else:** the rest of this page is written for your Muse, not for you. It is supposed to look technical, that is normal, and you do not need to read or understand any of it. Your only job is the copy and paste below, then following your Muse's short instructions. It will stop and hand things to you for every sign-up, code, password, and approval.


**How to use this file:** Open a new side chat with your own Muse assistant and paste this whole document in as your first message. Your Muse will then run the setup described below, doing the typing, installing, and checking for you. You stay in charge: you will personally do every account sign-up, every sign-in code, every password, and every approval. Nothing here asks you to paste a password or a secret key into any chat — if anyone or anything ever asks you to, stop.

**Just joined Muse? Redeem this code first — it takes ten seconds:** **2X7WMN**. Using this referral code upgrades you to **1 billion tokens — equivalent to about 2.5 months of usage — available right away**, and the tokens **can never expire**, so they sit there as a backup whenever you need them. How to redeem: in the **Muse app**, go to **Settings > Redeem token** (in the app, this option only shows during your **first 48 hours** after joining, which is why it is worth doing while you are here). On the **web at muse.ai**, go to **Settings > General > Usage > Redeem invite code**. Quick honesty note: this is the channel's referral code — the channel gets a small credit if you use it, it doesn't cost you extra, and the free route in this file works without it.

---

## Message to the Muse reading this

You are being asked to set up **Pi-hole** — a small, free program that blocks ads and trackers for a whole house — on a free cloud box, following the job list below. The one idea under the whole build: every device constantly asks a "phone book" (called DNS) where things live. Pi-hole sits at that phone book with a list of ad and tracker names. When a wanted name asks, Pi-hole passes the real address through. When an ad or tracker name asks, Pi-hole answers "nowhere" — and the ad never loads. The human you are helping is **not assumed to be technical**. Work in plain words. Explain each step before you do it, in one or two short sentences, and after each step tell the human what they should now see, so they can confirm it worked.

The design that keeps this free and safe: Pi-hole lives on the free cloud box and answers **only** through a private tunnel (WireGuard) between each device and the box. Only the tiny "where is this?" questions travel the tunnel — never videos or downloads — so the build stays far inside the free box's small data allowance (about 1 GB a month out on the small free Google box). Never "improve" this build by opening Pi-hole to the whole internet, and never widen the tunnel to carry all traffic.

**Your checkpoints — stop and hand over to the human at each of these:**

1. Creating any account (the cloud account for the free box, if they do not have one). The human creates accounts and does all identity checks themselves. Note: Google may ask for a card at sign-up only to check the person is real; the free box itself charges nothing — the human handles any card screen alone.
2. Any sign-in code, verification code, or password. The human types these. **Never ask the human to paste a password, API key, or key file into this chat.** That includes the Pi-hole control-page password and every WireGuard key. When a secret must be placed somewhere, the human types it directly into the place it belongs while you wait.
3. Any payment or card step. This setup is free; if a screen asks for payment, stop and hand it to the human.
4. Any approval prompt on the human's screen. Describe what it is asking; the human taps or clicks it.
5. The human must be physically present with their phone for the tunnel step: the phone's WireGuard key is delivered as a QR code shown on the box's screen, and the human scans it with their own phone. That code is a key — it is never sent through this chat, never screenshotted-and-shared, never posted anywhere.

**Your safety rules (do not bend these):**

- Pi-hole answers questions **only** on the tunnel and on the box itself. A blocker that answers strangers gets borrowed by strangers and can be used to bother other people's sites. If you test it from the open internet, the correct result is silence.
- One device, one tunnel, one code — never the same code on two devices. Each device gets its own fresh keys.
- A QR code for a tunnel is a key. Treat every code you generate as live the moment it exists.
- Secrets live in private files on the server, nowhere else — not in this chat, not in your notes.
- If a step fails, say plainly what failed, what you tried, and what you need from the human. Never report a step as done when it is not.
- Where the written guide and this file differ in any command, the guide's printed commands win — and where a project's own page (Pi-hole's, WireGuard's) disagrees with both, the project's page is right.

---

## The end state you are building

Whole-house ad blocking that the human owns outright:

- **Pi-hole (version 6, as tested by this channel)** running on a free cloud box — the box from Video #1, or the small free Google box the written guide uses. $0 a month.
- Pi-hole asking two big free phone books when it lets a name through: **Cloudflare and Quad9**, both ticked, so one can be down and the internet never notices.
- Pi-hole's door locked: it listens only on the tunnel and on the box itself. From the open internet it answers with silence — tested.
- **WireGuard**, the tunnel program, running on the box, listening on **UDP port 51820**, with exactly one firewall door opened for it.
- **The human's phone joined** by its own tunnel and its own QR code, with the handshake proven ("latest handshake: a few seconds ago"), and blocking measured with a public test.
- Every further device in the house joined the same way — one tunnel, one code per device (see the honest labels in the final report: this part follows the proven steps but was labelled **not tested yet** by the channel, which had run exactly one phone on its own setup when the video was made).
- The honest limit, told to the human plainly before you finish: ads served from the **same address as the show itself** cannot be separated, so the **YouTube app's ads stay, Instagram and Facebook feed ads stay, and most streaming apps' ads stay**. Anyone who promises a blocker that removes those is selling something that does not exist.

## Job list

Work through these in order. After each job, give the human a one-line status. The exact commands for the install steps are printed in order in the written guide ("Your Own Free Ad Blocker"); use those, not your memory.

1. **Prep.** Confirm the human has: a free cloud box (Video #1's box, or the small free Google box from the guide), their phone, the free WireGuard app installed on the phone, and about an hour. Explain the phone-book idea in plain words before starting.
2. **Open the box's typing window.** In the cloud console, use the SSH button next to the box — a terminal opens in the browser. Every command in this build is copy-and-paste from the guide; nobody types commands from memory.
3. **Install Pi-hole.** Paste the update line first and let it finish. Then paste the install line from Pi-hole's own official site (**install.pi-hole.net**), exactly as printed in the guide. A blue setup screen walks through questions one at a time. The answers that matter: yes to the admin web interface (the control page), yes to the default blocklist, defaults everywhere else. *Checkpoint: at the end the installer shows a password for the control page. The human saves it somewhere safe and private, like a house key — it is never typed into this chat. If it is ever lost, `pihole setpassword` in the terminal sets a fresh one.*
4. **Pick the two phone books.** In the control page, under Settings, then DNS, tick **Cloudflare** and **Quad9** and save. Checkpoint together: both names show ticked on that page. Nothing uses Pi-hole yet — the next jobs fix that, safely.
5. **Lock the door.** Set Pi-hole to listen only on the tunnel and on the box itself — nothing else. Explain why before you do it: an open blocker gets found by strangers and borrowed. This setting is never loosened later.
6. **Build the tunnel's box end.** Install WireGuard on the box with the pasted line printed in the guide. Then open exactly one door in the box's firewall: **UDP port 51820**, the tunnel's doorbell. Known pitfall, from the channel's own build: on the first try the tunnel would not connect at all — no error, just silence — because the firewall rule for that one door did not exist yet. Adding the rule brought the tunnel straight up. If a tunnel will not connect later, check the door before anything else. Checkpoint: run `wg show` in the terminal — the tunnel should be listed, listening on port 51820.
7. **Join the phone.** *Checkpoint: the human does this part in person, phone in hand.* On the box, make a fresh key pair for the phone — the phone's private half stays secret — and draw it as a QR code in the terminal with the command printed in the guide. The human opens the WireGuard app, taps +, taps "Scan from QR code," scans the square, names it something plain ("my-phone"), saves, and flips the switch on. Remind them: blocking only works while the switch is on, and it is fine to leave it on always — it carries only tiny questions, so it uses almost no battery and almost no data.
8. **Prove the handshake.** Back in the terminal, `wg show` again. Under the phone's entry, the human should see "latest handshake: a few seconds ago," with small amounts of traffic moving both ways. (On the channel's box, the first check read: handshake 16 seconds old, traffic already flowing.) If the handshake line is missing or old, the phone and box are not talking — re-check the switch, then the door from Job 6.
9. **Prove the blocking, with real numbers.** With the tunnel on, the human opens **superadblocktest.com** on the phone — a free public page that tries hundreds of known ad and tracker addresses and counts how many get through — and lets it finish. Then the comparison, once: tunnel **off**, test again (the score drops, ads return); tunnel back **on** (quiet again). That off/on check is the human's first fix-it tool forever. **How to state the channel's result, honestly:** on the channel's own phone, the night it was built, this setup blocked **84% — 410 of 482 checks**. The Brave browser alone scored 77%, and AdGuard, a paid blocker, also scored 77%. That 84% is the channel's measured result on its phone (which used Brave, part of why the score is high) — it is a test result, **not a promise**. A healthy build lands in the low-to-high eighties, and the human's number will vary with their browser.
10. **Test the lock from outside.** Ask Pi-hole a question from the open internet, the way a stranger would. The correct answer is silence. If it answers, stop and fix the lock from Job 5 before going any further.
11. **Add the rest of the house (labelled honestly).** For each further phone, tablet, or laptop: repeat Jobs 7–8 with fresh keys and the next address in line — the box makes that device its own key pair, its public half is added to the box's tunnel settings, its own QR code is drawn, and that device scans it. Name every tunnel for its device and owner from day one ("kitchen tablet," "mum's phone") — the day a phone is lost, the human deletes exactly that tunnel on the box and its key is dead forever. **Tell the human plainly:** the channel had run exactly one phone on its own setup when the video was made, so this job carries its **NOT TESTED YET** label — it follows the proven steps exactly, but the channel had not walked a second device yet. Two more honest labels ride along: per-device **groups** in the control page (stricter lists for kids' tablets, lighter for the human's phone) are a real feature the channel has **not tested yet**; and the **router shortcut** — pointing the home router at this cloud Pi-hole — is not a step at all: the router would ask from the open internet, the lock answers silence, and opening the blocker to everyone is a trade this build refuses to make. Do not set it up.
12. **Final report.** Give the human a plain-words summary: what is running and where, which devices are joined, their own test score next to the channel's 84% (labelled as the channel's test, not a promise), what it costs ($0/month), the honest limits (same-address ads stay — YouTube app, Instagram, Facebook, most streaming apps), and the honest labels that remain: second-device joins, groups, and the fix-it tools in the guide (allowlist, timed pause) are **not tested yet** by the channel — its own setup has not needed them. Close with the six rules below.

## The safety rules (read these to the human at the end)

1. Your QR code is a key — never post it, send it, or share a screenshot of it. If a picture of it ever escapes, delete that tunnel and make a fresh one.
2. One device, one tunnel — never the same code on two devices.
3. Your control-page password is private, not reused from anywhere else, and never typed into a chat.
4. Pi-hole stays behind the tunnel — never open to the internet, no exceptions.
5. Lost phone? Delete its tunnel on the box — its key is dead forever.
6. Leave the tunnel on — blocking only works while it is on.
7. Secrets live in private files on the server — never in a chat.

*This file matches the video "How to Block Ads on Every Device With Pi-hole" (Video #3 of the Let Muse Build It series) and the written guide "Your Own Free Ad Blocker" ($9) — the guide's Level 1 build covers the first phone; this file carries the build through the whole house. Where this file and a project's own page disagree (install commands change), the project's page is right.*

