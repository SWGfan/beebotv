# Beebo public feature, control and capture catalogue

**Purpose:** a source-backed production checklist for public feature pages, screenshots and walkthrough video. It records what is present in the source or released web files as of 2026-09-20. It is deliberately not a marketing brief: an item may be implemented but still need a release, test, capture, legal review or service configuration before it can be advertised as available.

## Rules for public pages

1. Use only the public name shown here. Do not use console, ROM, emulator, PS2, N64 or third-party game-library language.
2. A promotional illustration is never labelled a product screenshot.
3. Capture from the current signed-in sample account and current release build. Remove personal media, e-mail addresses, Wi-Fi names, QR codes, IP addresses, passwords and tokens before approval.
4. Mark an item **Pilot / not released** until it has a shipped build, working backend and end-to-end test. A source file alone does not establish a public service.
5. Use the existing download metadata (`desktop-version.json` and `downloads/app-build.json`) for every download panel. Do not hand-type a version, date or time.
6. Do not promise a feature that is not listed as **Released** below. In particular, do not promise a browser Watch Together video player, child-content filtering, title requests, cloud hosting, integrated commercial live TV, VPN service, rewards offers, or game hosting before their separate launch checks are complete.

### Status key

| Status | Meaning | Public wording now |
|---|---|---|
| Released | Listed in the current downloadable release metadata or existing live public flow | Describe what the released build does, after capture approval. |
| Implemented — capture required | Present in source but needs a fresh sample-account capture and feature test | Keep out of feature-page claims until captured and tested. |
| Implemented — service launch required | Present in source but relies on backend, paid plan or infrastructure that is not launched | Describe only as **in development** if a page is needed. |
| Planned / do not publish | Documented design or desired capability with no public-ready implementation | Do not put on public feature pages. |

## Release source of truth

| Product | Current public metadata | Download route | Evidence |
|---|---|---|---|
| Windows desktop | Beebo `0.1.54`, released Sep 20, 2026, 4:20:14 AM Eastern | `https://origin.beebo.tv/downloads/BeeboEntertainmentSetup-0.1.54.exe` | `desktop-version.json` |
| Android | Beebo `1.35` (build 36), released Sep 20, 2026, 4:14:23 AM Eastern | `https://origin.beebo.tv/downloads/BeeboEntertainment-v1.35.apk` | `downloads/app-build.json` |

Every public product page should use two side-by-side download panels: **Windows desktop** and **Android app**, showing version, release date/time, file type and a What’s new link. Product-only sites may link to these panels instead of duplicating unrelated downloads.

## Desktop app catalogue

| Public feature | Entry point / visible control | What a capture must prove | Status and wording limit |
|---|---|---|---|
| First-time setup | Sidebar: **Get Started** | Owner account step, selected media folders, QR phone connection, away-from-home address panel | Released; do not expose the real address or QR code. |
| Library folders | **Choose Movies folder**, **Choose TV Shows folder**, **Beebo Inbox**, **Open folder** | Folder selection with only Beebo sample folders; destination path visible only if non-sensitive | Released. Explain that Beebo scans folders selected by the owner. |
| Movies | Sidebar: **Movies** | Poster grid, search/sort or title detail using Beebo-owned sample media | Released / capture required. Do not use unlicensed film posters or personal library. |
| TV shows | Sidebar: **TV Shows** | Show detail and episode list, including a clearly labelled missing episode if it is present in the current build | Released / capture required. |
| Phone backups | Sidebar: **Phone Backups** | Backed-up phone gallery with a non-personal sample image/video | Released; use the current label, not the former plain “Photos” label. |
| Video playlists | Sidebar: **Video Playlists** | A saved rule and the matching title list | Released / capture required. A playlist may contain films; it is not a music-only list. |
| Upload | Sidebar: **Upload**, drop zone, **Clear upload history** | Upload history clear confirmation and a subsequent list without deleting source video | Released / capture required. State precisely: clears history records, not media files. |
| Dashboard | Sidebar: **Dashboard** | Library counts and account summary with non-personal sample data | Released / capture required. |
| Admin / users | Sidebar: **Admin** and **Users** | Add/approve/revoke user, away-access state; redact all names/e-mail/IP data | Released / capture required. Do not claim parental content filtering. |
| Watch history | Sidebar: **Watch History** | Per-profile history using sample media | Released / capture required. |
| Flags | Sidebar: **Flags** | A flagged unplayable sample file and owner review action | Implemented — capture required. Do not call it a title request. |
| Converted | Sidebar: **Converted** | A completed conversion entry and original-versus-output indication | Implemented — capture required. Do not promise an unlimited transcode count. |
| Missing files | Sidebar: **Missing Files** | Missing sequel/episode/title card and allowed search action | Implemented — capture required. The feature helps locate a title; it does not download media. |
| Help me choose | Sidebar: **Help me choose** | Surf recommendations by mood, era or type | Implemented — capture required. |
| BeeboSchool | Sidebar: **BeeboSchool** | Parent PIN and a sample lesson/report card with invented student data | Implemented — capture required. Do not market as library content filtering. |
| Settings | Sidebar: **Settings** | Non-sensitive preferences and settings backup/restore flow | Implemented — capture required. |
| Sign out | Sidebar footer: **Log out** | Confirmation and returned sign-in state | Released; no sensitive account shown. |
| Release details | Sidebar footer: version, **What’s new** | Current version and timestamp matching shared metadata | Released. |

## Android app catalogue

| Public feature | Entry point / visible control | What a capture must prove | Status and wording limit |
|---|---|---|---|
| Connect to a Beebo computer | Setup: **Scan QR to connect**, **Change server address** | Sample QR scan or address entry; no real LAN address/QR remains in final image | Released. Explain same-Wi-Fi setup separately from away access. |
| Movies and TV | Bottom navigation: **Movies**, **TV** | Poster grid, title details, playback screen and cast row with Beebo-owned sample content | Released / capture required. |
| Missing episodes | TV show detail: **Missing episodes shown** / **Show missing episodes** | Missing episode card plus the informational sheet and permitted search path | Implemented — capture required. It locates information and opens a selected external search; it does not provide the missing episode. |
| Cast and actor discovery | Title detail: **Cast**; actor page missing-title list | Actor detail, owned titles and missing film/show list using only sample metadata | Implemented — capture required. Any Google/custom search capture must not suggest that Beebo hosts or supplies the missing work. |
| Chromecast / Google TV | Top app bar: cast icon | Phone selecting an available compatible receiver on a safe test network | Implemented — capture required. Do not promise away-from-home casting if the app blocks it for the current route. |
| Continue Watching | Bottom navigation: **Continue** | Progress card, resume action and a sample title | Released / capture required. |
| Downloads | Bottom navigation: **Downloads** | Download state, offline availability and resume behaviour with Beebo sample media | Implemented — capture required. |
| Surf | Bottom navigation: **Surf** | Mood/era/type selection and resulting recommendation | Implemented — capture required. |
| Campsite shortcut | Golden tent in the top app bar; content description: **Open Campsite Mode** | Entering Campsite Mode from the top icon | Implemented — capture required. |
| Campsite Mode | **Start Campsite Mode**, hotspot/joining QR flow, guest browser | Host screen, generated QR, guest browser playback and roster; use a temporary sample network | Implemented — capture required. It uses the host phone/hotspot; do not conflate it with Watch Together. |
| Guest games | Campsite/Play: **Campsite games**, **Invite players** | At least two guest phones in a room where the actual game supports guests | Implemented — capture required. |
| Watch Together | Player / room flow: **Watch Together** | Two signed-in devices on the same Beebo account, same title, pause/seek synchronization and re-sync behaviour | Implemented — capture required. Do not show or claim browser guests receive synchronized video. |
| Story Mode / BeeboBook | Other > **Stories**, title screen, **Prepare computer voices**, **Read aloud** | Story selection, character-name editor, approved available voice choice, read-aloud state | Implemented — capture required. The public page is image-led; do not claim any specific voice vendor or rights until separately cleared. |
| Outdoor tools | Other > **Outdoors**: star chart, nearby, Junior Ranger badges, trip recap, packing list, campfire mode, scavenger hunt | Individual sample screens with no precise location revealed | Implemented — capture required. Capture location-related features only using a safe, coarse test location. |
| Phone sharing in campsite | Campsite shared photo/video host flow, swipe next/previous | Host selects Beebo-owned test media; a guest device visibly follows next/previous movement | Implemented — capture required. Confirm all participants receive the sync before publish. |
| Phone backups / Space Saver | Phone backup area, browse backed-up media | Wi-Fi-only preference, confirmation before any deletion, and backup gallery using sample assets | Implemented — capture required. Do not state that a phone copy is deleted automatically. |
| Read It To Me | Other > **Read It To Me** | Pasted Beebo-authored sample text, voice controls and offline output | Implemented — capture required. |
| Official Free TV | Other/Tools route: **Official Free TV** | One official-source card, external-service confirmation, country/availability notice | Implemented — service/legal review required. Only list broadcasters after the official URL, availability and linking/embedding terms have been checked. Never capture or frame it as re-streamed inside Beebo. |
| Beebo Points Rewards | Other > **Beebo Points Rewards** | Disabled-by-default opt-in state, saved-balance explanation and a no-offer state | Implemented — service launch required. No real ads, offers, points value, cash-out or pricing claim before provider, consent and server-side verification launch. |
| Account controls | Other > account: **Sign out**, **Delete my account** | Non-personal test account sign-out and deletion confirmation sequence | Implemented — capture required. |

## Browser catalogue

| Page / entry point | Current public purpose | Required capture or video clip | Status / restriction |
|---|---|---|---|
| `index.html` | Beebo overview, feature navigation and downloads | Desktop + mobile hero, download panels, feature navigation | Released; use only current metadata. |
| `server-setup.html` | Windows installation and setup guide | Fresh Windows sample account: download, install, account creation, folder selection, QR connection | Released guide; no personal folder names. |
| `app-on-your-phone.html` | Android install and phone setup guide | Android download, install, safe sign-in and first connection | Released guide. Do not call it Google Play until Play release exists. |
| `visual-tour.html` | Product visual tour | Approved app and desktop screenshots, each labelled with product/version | Released page; replace any unverified imagery. |
| `watch-away-from-home.html`, `stream-anywhere.html`, `direct-connection.html` | Remote connection explanations | Direct-versus-relay route banner with test account; browser/mobile safe address | Released informational pages; exact available route must match live product behavior. |
| `beebo-relay.html`, `own-relay.html`, `open-ports.html` | Relay, own-relay and router education | Diagram or non-sensitive setup capture | Existing guide content; do not say a paid relay/VPN service is live until it is deployed and tested. |
| `photos.html`, `music.html`, `playlists.html`, `quality-and-subtitles.html`, `cast-to-tv.html`, `posters-and-info.html` | Feature-specific guidance | A single focused screenshot per visible button/action | Existing public guides; source and capture must be revalidated before expansion. |
| `story-writer.html`, `computer-voices-setup.html` | Story and desktop voices help | Story page, character customization, voice preparation UI | Existing public guides; do not use third-party voice claims without licence confirmation. |
| `car-companion.html`, `driving-safety.html` | Android Auto / car companion safety guidance | Audio-only car capture and sound/latency control; no moving video on driver display | Existing public guide; keep safety wording prominent. |
| `manage-users.html`, `privacy.html`, `terms.html`, `delete-account.html` | Account, privacy, terms and deletion information | A clear non-personal management UI capture; no individual data | Existing legal/help pages; legal review needed before commercial launch. |
| `updates.html` | Release notes and download/version release details | Two-panel Windows/Android releases; page-top return control in final design | Released. |
| `games.html` and `games/<slug>.html` | Game index and individual instructions | Only approved real game captures; see game matrix below | Not yet a released complete catalogue. Do not publish a game page as complete without its approved capture. |

## Games: source-backed inventory

**Source:** `GAME-CATALOG-INVENTORY.json`, generated from Android `CampsiteGameCatalog.ALL` and `.SOLO` on 2026-09-20. It finds **39 campsite games + 4 solo games = 43 implemented games**. It confirms a bot-move implementation in each campsite game source, but a public bot-play claim needs an actual selector and end-to-end test. Guest-required games must never claim bot matches.

### Public naming guardrails

- Use **Drop Four**, never Drop Four or Drop Four.
- Use **Sea Battle**, never Battleship.
- Use **Reversi**, not Othello; **Crazy Eights**, not UNO; **Pairs**, not Memory; **Snakes and Ladders**, not Chutes and Ladders.
- Every game title, artwork, page copy, metadata and browser preview needs commercial naming/art review before broad launch. Generic names in source are not legal clearance.

| Category | Implemented public titles | Play evidence | Capture set required before its individual public page |
|---|---|---|---|
| Board / strategy | Checkers; Chess; Dominoes; Dots and Boxes; Five Dice; Drop Four; Ludo; Mancala; Nine Men’s Morris; Reversi; Sea Battle; Snakes and Ladders; Tic-Tac-Toe | Host can start; bot-move source present. Guest feature needs actual room test. | Menu tile, setup, in-play, result. Sea Battle additionally needs drag/drop ship placement, legal shot, hit/miss and result without exposing both boards. Dice games need on-board rolling animation plus settled result. |
| Cards / matching | Crazy Eights; Go Fish; Old Maid; Pairs; Snap; War | Host can start; bot-move source present. | Menu tile, player hand/board, meaningful action, result. |
| Outdoor | Car Bingo; Sight Race; Nature Bingo | Host can start; bot-move source present. | Prompt/card, marked progress, result. Use generic safe outdoor details. |
| Party — host can start | Classic Bingo; Hot Potato; Movie Trivia; Rock Paper Scissors | Host can start; bot-move source present. | Lobby, action/reveal, score/result. Movie Trivia must use Beebo-authored or licensed questions in browser previews. |
| Party — guests required | Campfire Werewolf; Fake Out; Pick the Next One; Sketch & Guess; The Quiet Game; Two Truths and a Lie; Who’s the Spy? | Game catalogue requires guests. | Lobby, guest-phone state, room action/reveal and result. Never advertise bot play. |
| Word / talk — host can start | Campfire Stories; Category Chains; Story Builder | Host can start; bot-move source present. | Prompt, contribution or turn state, completed result. |
| Word / talk — guests required | Twenty Questions; This or That; Tough Choices | Game catalogue requires guests. | Guest-specific prompt, votes or questions, room result. Never advertise bot play. |
| Solo puzzles | Five Letters; Hidden Mines; Patience; Number Grid | Solo games in source. | Main board, meaningful play state, completion/result. |

### Game-page controls to document only after verification

| Control / interaction | Page capture needed | Restriction |
|---|---|---|
| Start a game / choose category | Games screen and game lobby | Needs current build test. |
| Invite guests / QR join | Campsite host and at least one guest phone | Do not show real joining code or Wi-Fi credentials. |
| Play against Beebo | Bot selector plus completed match | Never use for a guest-required title. |
| Drag and drop ships | Sea Battle setup | Do not reveal the opponent’s hidden ship layout. |
| Roll 3D dice | In-game board while rolling and stopped | A still illustration does not prove an animated roll. |
| Vote / draw / submit answer | Actual guest-room interaction | Needs two or more participant devices. |
| Restart / next round / result | Result screen and reset state | Confirm the visible wording and outcome. |

## Privacy, access and paid-service catalogue

| Capability | Publicly safe description today | Status / condition | Capture required |
|---|---|---|---|
| Local home viewing | Home viewing from selected folders remains local to the owner’s Beebo computer and home network. | Released. | Home connection banner and a sample title. |
| Household members | A household can have up to 6 members, including the owner. | Product policy in current work; end-to-end cap must be validated before release copy. | User management and household member count. |
| Remote viewing control | Owner-controlled limit is planned at 1–4 simultaneous away-from-home streams, default 4. | Implemented / service launch required; enforce in the live service before public claim. | Owner setting, four active sample sessions or reliable test harness, fifth-session message. |
| VPN household limit | Planned: 6 registered devices, up to 4 connected at once per household. | Implemented / service launch required; requires live subscription, entitlement and VPN deployment. | VPN device list, four-session limit and a safe fifth-device message. |
| Beebo VPN pricing | Proposed CA$2/month with multi-month discounts. | Planned / billing configuration required. Never show a price as purchasable until Stripe product, tax, terms, cancellation and support paths work. | Checkout, invoice, device enrollment and cancellation workflow. |
| Beebo Relay | Route selection can identify direct connection, Beebo Relay or Cloudflare Relay when known. | Current Android release notes reference route identification; paid relay plan/service status must be confirmed before commercial claim. | Mobile connection banner for direct and relay test cases. |
| Adult-profile privacy | A profile owner may protect viewing-history visibility while household owner sees permitted aggregate usage. | Implemented / security and product launch required. It must be password-protected and independently tested before public claim. | Profile privacy setup, owner aggregate-only dashboard, blocked history attempt. |
| Private uploaded folders | Design supports a user-owned folder/password workflow and recovery options. | Implemented / security and deployment review required. Do not promise encryption or owner-proof secrecy unless independently verified. | Folder setup, lock/unlock, recovery consent and failure states. |
| Beebo Points Rewards | Optional, disabled by default; points balance remains when a person opts out. | Implemented / provider, consent and service launch required. | Opt-in, opt-out, balance retention, offer detail fields. |
| Official Free TV | Directory opens broadcaster-owned services; Beebo does not host the channel stream. | Implemented / per-broadcaster legal and availability review required. | Official-source card, external-service confirmation and territory notice. |
| Antenna / tuner TV | Personal local broadcast tuner support. | Planned / do not publish. | None until hardware support ships. |
| Licensed integrated FAST channels | Beebo-hosted guide/player with supplier rights. | Planned / do not publish. Requires distribution agreements, geo rules and ad reporting. | None until rights and service launch. |
| Managed hosting / game hosting | Future hosting products. | Planned / do not publish as available. | None. |

## Capture and walkthrough production order

1. **Fresh sample identity:** create and use a dedicated Beebo sample owner account with only Beebo-owned videos, images, names and metadata. Never record a personal library.
2. **Desktop video:** download Windows installer; install; create account; select Beebo sample folders; demonstrate the two QR panels; show movies, TV, missing entries, cast/actor discovery, playlists, phone backups, upload-history clear, user controls and log out.
3. **Android video:** download the verified APK from the public site; install; sign in to the sample account; scan the safe temporary QR; show Movies, TV, missing episodes, cast, Continue, Downloads, Surf and route banner.
4. **Campsite video:** use a separate temporary hotspot; show Campsite Mode QR, guest browser video and guest games. Delete/revoke temporary hotspot details after filming.
5. **Watch Together video:** two signed-in sample devices, same title. Show play/pause/seek/re-sync; state on-screen that it is app-to-app on the same Beebo account.
6. **Stories and outdoor tools:** record neutral sample story/voice interface and safe test activity screens without location information.
7. **Game capture sprint:** follow the 43-game matrix; record genuine screens only. Begin with Drop Four, Sea Battle, Five Dice, Chess, Movie Trivia, Campfire Werewolf, Sketch & Guess, Story Builder, Five Letters and Patience.
8. **Accessibility and approval:** record Android model/OS and app version, desktop version, capture date, source screen, alt text and reviewer approval in `assets/games/captures.json`. Convert approved originals to WebP only after review; keep originals out of the public web root.

## Explicit exclusions for the public catalogue

Do not place these on feature pages, comparison charts or download panels until the named release gate has passed:

- Console emulation, ROMs, PS2, N64 or any third-party console content.
- Unverified “play against Beebo” claims for a particular game.
- Any third-party channel embedded/rebroadcast inside Beebo without rights.
- Browser guest video in Watch Together.
- Child-safe library filtering or content controls.
- Media title request/download functions.
- Live server locations, user counts, precise traffic/usage, IPs or household location.
- VPN, rewards, hosted games, managed hosting or new regions as live purchasable services before their service, billing, security, support and monitoring checks are complete.

## Primary evidence locations

- Website content guardrails and established feature evidence: `Beebo-Website-Content-Brief.md`.
- Current Windows release metadata: `desktop-version.json`.
- Current Android release metadata: `downloads/app-build.json`.
- Game inventory: `GAME-CATALOG-INVENTORY.md` and `GAME-CATALOG-INVENTORY.json`.
- Individual-game public page requirements: `GAME-PAGE-BUILD-PLAN.md`.
- Android navigation and visible labels: `D:\MovieAPP\JenkinsAPP-github\apps\core\app\src\main\java\com\beeboentertainment\movie\ui\MainActivity.kt`, `ui\screens\PlayMoreScreens.kt`, `ui\screens\TvScreen.kt`, `ui\screens\ActorScreen.kt`, `ui\screens\OfficialFreeTvScreen.kt`.
- Public-status safety boundary: `owner-operations\PUBLIC-STATUS-PAGE-SPEC.md`.
