# Beebo Entertainment — website content brief

Written 2026-09-10. **Every claim below was traced to code before it was written down.**
Anything the old site said that turned out not to be true has been removed, and the four
worst offenders were fixed on the live site tonight (listed at the end).

Use this as the source of truth if you have ChatGPT redo the site. Give it this whole file
and tell it: *"Only make claims that appear in this document."* That one sentence is what
stops a rewrite from quietly reinventing the features that got us in trouble.

---

## The one rule

**Do not let a rewrite invent features.** The old site sold a kid-safe mode and a
"request a title" button. Neither exists. Nobody lied on purpose — the site got written
from a plan, and the plan moved. A rewrite from an old page will reintroduce every one of
those claims, because they read like they're already true.

---

## What Beebo actually is

You point Beebo at the folders where your films and shows already live. It builds a proper
library out of them — posters, cast, descriptions — and serves it to every screen in the
house. Away from home it reaches your PC directly, without you touching your router. Your
files never leave your computer.

$0.99/month. 30-day free trial, no card.

---

## Verified feature list

### The library
- Point at folders; Beebo builds the library — posters, cast, descriptions, pulled from TMDB
- Tidies messy filenames, sorts films from episodes, spots duplicate copies
- Continue Watching, per person, on every device
- Subtitles, from `.srt`/`.vtt` files sitting next to the video
- Mark where the intro ends once, and Beebo skips it for the whole household from then on
- Quietly converts anything a device can't play, in the background, one job at a time.
  The original file is never touched
- Can't decide? **Surf** picks something for you by mood, era or type

### Watching
- Phones, tablets, laptops, TV. As many at once as you like — there's no device limit
- Cast to a Chromecast or Google TV; the phone becomes the remote
- Picture-in-Picture, and audio that keeps playing with the screen off
- Download films and episodes to a phone or tablet for a flight or a dead zone.
  Downloads resume where they stopped
- No app needed: any browser on the same Wi-Fi gets the full library

### Away from home
- A free permanent web address, `yourname.beebo.tv`
- **No port forwarding, no router changes.** Beebo brokers a direct connection between
  your device and your PC. Only the handshake touches our servers — never the video
- Away-from-home address installs to your phone's home screen like an app
- HTTPS with real certificates, generated for you

### The people in your house
- Everyone signs in with their own account
- Add someone yourself, or let them request access and approve it
- Sign in with a password or a code, your choice
- Per-person watch history and stats
- Revoke or delete anyone in one click
- Repeated wrong passwords lock the account and email you about it

### In the car and off the grid
- **Beebo Auto** — your library's audio through the car speakers over Android Auto.
  Audio only, by design: no video on the driver's screen, ever
- **Watch Together** — everyone's screen stays in sync with the host's. Pause, seek,
  play, all mirrored, with a re-sync every few seconds
- Per-person audio-delay slider, so phone audio lines up with car speakers
- Passengers can scan a QR to join the room in a browser — no app, no account —
  for the **party games, reactions and roster**
- **Eleven party games** synced across the room: This or That, Movie Trivia (generated
  from your own library), Would You Rather, 20 Questions, Scavenger Bingo, Story Builder,
  Category Chains, The Quiet Game, Pick the Next One, plus a solo bot opponent
- **Campsite Mode** — your *phone* becomes the server. Guests scan a QR and watch over
  your hotspot with no internet, no app and no account
- Camping extras: star chart, scavenger hunt, packing checklist, Junior Ranger badges,
  a trip recap card, campfire ambience

### Extras
- **BeeboSchool** — kids' lessons, add-a-child, and a report card behind a parent PIN
- **BeeboBook** — read-along storybooks included; write your own with a private AI that
  runs on your own PC (optional, needs Ollama installed)
- **Space Saver** — move photos and videos off a full phone onto your PC. Wi-Fi-only by
  default; nothing is deleted from the phone until the PC confirms it has a copy; browse
  what you backed up from the phone afterwards
- **Read It To Me** — paste any text and the phone reads it aloud, offline

---

## Things that are true and the old site never mentioned

These are free marketing. Several are better than what's already on the page.

1. **Campsite Mode.** The phone itself becomes the server, over your own hotspot, with no
   internet at all. This is the strongest off-grid story in the product and the site is
   silent on it.
2. **Eleven party games**, room-synced. The site says "games".
3. **Full owner admin from your phone** — users, requests, flags, history, settings.
4. **Space Saver's gallery** — browse everything you backed up, from the phone.
5. **Read It To Me.**
6. **Flag a bad file** — a viewer reports a bad or unplayable copy and it lands on your list.
7. **Offline TMDB prefetch** — cache the artwork before a trip so the library still looks
   right with no internet.
8. **Settings backup and restore** to a single file.
9. **Trip extras** — star chart, scavenger hunt, badges, recap card.

---

## The two QR codes - don't mix them up

This tripped me up and it will trip up a copywriter too. Beebo has **two** separate
"scan a code, no app, no account" flows, and only one of them shows video.

**Campsite Mode** - `campsite/CampsiteServer.kt`. Your phone becomes the server. Guests join
your phone's hotspot, scan the QR, and **watch the film in their browser**. Real video, real
seeking (the server implements HTTP Range properly), sound and all. No internet, no SIM, no
account, nothing installed on the guest's phone. The host screen even lists who's watching.
**This is tested and working.** It is the most impressive thing Beebo does and the site
barely mentions it.

**Watch Together room** - `hub/public/party.html`, reached at `hub.beebotv.com/party/<code>`.
A guest who scans this gets the roster, the party games and emoji reactions. There is no
video player on that page. Keeping everyone's playback in sync is app-to-app, between
devices signed in to the same Beebo account.

So "scan a code and watch with no app" is **true** - say it, it's a great line - but it's
Campsite Mode, over your own hotspot. Don't attach it to the car sync section.

---

## Do NOT claim these

| Don't say | Why |
|---|---|
| Kid-safe mode, parental controls, content filtering | There is no code that filters a library for a child. A half-built store exists on the server; nothing reads it. **This is the most exposed claim on the site.** |
| "Request a title" / "their own request line" | No request button exists. What exists: Beebo notices a missing next-episode or sequel and files it for you |
| A browser guest can join a **synced Watch Together room and see the video** | The hub's guest page is a roster, party games and reactions - there is no video element in it. Sync is app-to-app. **This is not the same as Campsite Mode** - see below |
| Watch Together on laptops | There is no browser watch-party client. App-to-app only |
| "On Google Play" | Neither app is on Play yet — fixed on car-companion.html tonight |
| Pull media in from a USB stick | The importer is a PowerShell script with no UI — removed tonight |
| "Install app" from your **home Wi-Fi** address | The local server serves no web manifest, so Chrome won't offer to install. Only the `.beebo.tv` address installs properly |
| "None of this is visible on the internet" | An admin-flagged account can reach an owner console over your secure address. Reworded tonight |

### Two more worth knowing
- **Watch Together needs every device signed in to the same Beebo account.** Not a bug,
  but say it, or people will try it with a friend's account and think it's broken.
- **If the host switches to a different film, viewers don't follow.** Everyone opens the
  same title, then syncs. Worth a line in the fine print rather than a support email.

---

## Fixed on the live site tonight

1. `index.html` — "Family accounts & kid-safe" → "Family accounts you control", describing
   what actually ships (approve, watch stats, revoke)
2. `index.html` — pricing bullet, same change
3. `index.html` — "Ask for anything" → "Beebo spots what's missing"
4. `index.html` — guest QR card now describes **both** guest paths: Campsite Mode (guest watches the film in a browser over your hotspot, no internet) and a Watch Together room (games, reactions, roster)
5. `index.html` — USB-stick claim removed; APK size ~7 MB → ~17 MB; version placeholders
   0.1.15 → 0.1.18
6. `car-companion.html` — two "On Google Play" badges → "Download from this site"
7. `manage-users.html` — the flat "No" about internet visibility now explains the admin console

Every edited page was re-checked for well-formed HTML. `.bak` copies sit beside each one.

---

## If ChatGPT rebuilds the site

Worth doing — the content is stronger than the current presentation, and Campsite Mode
alone deserves a page. Three things to hold onto:

- **Keep `site.css` and its variables.** The colour tokens and type scale are consistent
  across 23 pages. A rewrite that invents its own palette means re-doing all 23.
- **Keep the page filenames.** They're linked from inside the app and the desktop app.
  New pages are fine; renaming existing ones breaks live links.
- **Feed it this file and nothing older.** Any older page will reintroduce kid-safe.

Lead with the things nobody else has: no port forwarding, the phone as a server at a
campsite, eleven synced games in the car, and $0.99 a month against Plex's pricing.
