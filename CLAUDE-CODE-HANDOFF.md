# Beebo Engineering Handoff for Claude Code

**Prepared:** September 20, 2026  
**Owner direction:** Finish the Windows + Android Beebo products first. Do not start Apple, Linux, TV, managed hosting, game hosting, rewards, or new regional services until the core product, paid access, privacy, connection routes, and release workflow are complete.

## Read this first

This repository and the product are actively changing. Preserve existing work. Do **not** run destructive Git commands (`reset --hard`, `clean`, force push) or overwrite unrelated files.

Be accurate in public copy:

- Do not claim a feature is live merely because source code exists.
- Do not publish personal media, private IPs, Wi-Fi names, QR values, passwords, tokens, e-mail addresses, real household details, or unlicensed film/TV artwork.
- Do not mention console emulation, ROMs, PS2, N64, or third-party console content in public Beebo pages.
- Use `4-in-a-row` as the public game name. Internal class/route names such as `ConnectFourGame` may remain technical implementation details.
- Do not claim integrated TV channels unless Beebo has distribution rights. The current Official Free TV screen must launch the broadcaster’s own official service externally; it must not host, re-stream, or embed the channel.
- Do not market VPN, relay, paid plans, rewards, game hosting, cloud hosting, or regional availability as purchasable until configuration, security checks, end-to-end testing, support material, and release approval are complete.

## Product decisions already made

### Household, price, and limits

| Product | Decision |
|---|---|
| Beebo household | Up to 6 people/profiles per household. |
| Away-from-home streaming | CA$3/month per household. Direct connection is always attempted first; Beebo Relay is included when it is available. At-home use remains free. |
| Away stream concurrency | Maximum 4 simultaneous away-from-home video streams per household. At-home viewing does not count. |
| VPN | CA$2/month per household, up to 6 registered devices/people and maximum 4 devices online simultaneously. |
| Future term discounts | User wants 3-, 6-, and 12-month discounts, but exact discount percentages are not decided or configured. |
| VPN/relay approach | Must be secure, login-gated, paid-entitlement-gated, direct-first, and report the actual route accurately. |

### Privacy and family controls

- Adult-profile privacy must require its own password, sign the profile out on other devices when enabled, block owner profile-switch shortcuts, and use that person’s e-mail for recovery.
- Private folders are intended to be password-protected/encrypted for the individual user. Folder setup should offer recovery e-mail to the folder owner and an optional owner-account recovery copy. This needs a security design and implementation review before release.
- Owners should retain aggregate operational information such as bandwidth; adult-history privacy must not expose titles/history to the household owner.
- Never send or display a recovered password by e-mail. Use time-limited reset links/tokens, rate limits, audit logging, and notification to the folder owner. An owner recovery copy should authorize a reset path, not reveal the password.

### Library and setup direction

- Default storage direction: `C:\BeeboEntertainment` with subfolders for library, uploads/inbox, phone backups, and user-owned areas; the owner must be able to choose any destination.
- Setup should offer: scan selected computer locations for videos/photos; let the owner choose whether to organize into a chosen destination; explain that metadata matching can miss incorrect filenames; recommend organizing all selected media and then using rename/metadata tools.
- Personal libraries must not be used in public demos. Use only Beebo-owned sample media in `BeeboSample` account/folders.

## Primary project locations

| Purpose | Location |
|---|---|
| Windows desktop / worker / VPN source | `D:\MovieAPP\JenkinsAPP-github` |
| Public websites | `D:\MovieAPP\beebotv` |
| Android app | `D:\MovieAPP\JenkinsAPP-github\apps\core\app` |
| Worker | `D:\MovieAPP\JenkinsAPP-github\worker` |
| VPN desktop | `D:\MovieAPP\JenkinsAPP-github\vpn\desktop` |
| VPN server | `D:\MovieAPP\JenkinsAPP-github\vpn\server` |

## Implemented work awaiting integration, release or end-to-end validation

### 1. Official Free TV directory — Android

Added `apps/core/app/src/main/java/com/beeboentertainment/movie/ui/screens/OfficialFreeTvScreen.kt`, wired in `PlayMoreScreens.kt` and `MainActivity.kt`.

- Uses external HTTPS links to broadcaster-owned services such as Global News, CTV News and TVO.
- No WebView, embedded player or re-streaming.
- A focused `OfficialFreeTvScreenTest.kt` was added.
- Keep CBC and any other broadcaster off the list until its current official availability/licensing position is verified for the target country.

**Blocker:** Full Android Gradle compile was not completed. This computer’s default Java is 8; project requires Java 17. Android Studio JBR Java 25 is incompatible with the project’s current AGP 8.5.2. Use a compatible JDK 17. A later targeted test was also blocked by a Gradle wrapper `.zip.lck` file held by another process.

### 2. Away-from-home capacity enforcement

A 4-away-stream household cap has been added to the Worker/RTC design.

- Worker: `worker/worker.js`, `worker/REMOTE-STREAM-CAPACITY.md`
- Host: `desktop/apps/desktop/resources/beebo-rtc-host/beebo-rtc-host.js`
- An opaque viewer/stream lease is created only after a signed-host video response; browsing, sign-in, WebRTC offers and at-home playback do not consume a slot.
- The fifth away viewer receives `429` with header `x-beebo-remote-error: away_stream_limit` and this exact customer message:
  `All 4 away-from-home viewing spots are in use. Ask someone in your household to stop watching, then try again.`
- Leases renew/release around actual viewing. Current lease length is 90 seconds.
- Worker tests passed at the time of work: `186/186`.

Android client mapping was added:

- `apps/core/app/src/main/java/com/beeboentertainment/movie/player/RemoteStreamCapacity.kt`
- `PlayerActivity.kt` now detects only the documented HTTP 429/header combination through the Media3 causal chain, so unrelated throttling still uses normal error text.
- Focused test: `RemoteStreamCapacityTest.kt`.

**Critical limitation:** The cap currently applies per VPN/relay server. Before multi-region launch, replace this with a strongly consistent central lease/reservation store so a household cannot use four slots per region.

### 3. VPN entitlement, registration, and device/session groundwork

Worker:

- `/auth/vpn-login` accepts `{email,password,publicKey}` and returns a short-lived token bound to that WireGuard public key.
- `/vpn/verify` validates token + public key.
- Uses exact entitlement metadata `beebo_plan === 'beebo-vpn'`; fail closed if not entitled.
- Relevant documentation: `vpn/desktop/ACCOUNT_LOGIN.md`.

Desktop client:

- Uses DPAPI encrypted pending key storage before sign-in; uses the exact same public key for registration.
- Tokens/passwords are not sent to renderer/unprotected state.
- Previous test result: 45 passed, 0 failed; 3 privileged helper tests skipped because helper was not built.

VPN server:

- `vpn/server/src/app.js`, `store.js`, `config.js`, tests.
- 6 registered devices per household; 4 active online session leases.
- Session claim duration is 180 seconds; renewal is based on WireGuard handshake activity.
- Fifth concurrent device receives `409 household_concurrent_device_limit` with `Retry-After`.
- Previous API/entitlement tests: 30/30 passed.
- Full test suite had three pre-existing Windows failures because a Bash bootstrap script expects `/bin/bash`.

**Still required before any VPN launch:** a real WireGuard tunnel, key provisioning/security review, live checkout entitlement, network kill-switch/DNS leak testing, automatic updater signing, server monitoring, customer terms/privacy/support, and multi-region central capacity enforcement.

### 4. Accurate Android connection wording

The phone must never say “Direct connection” if it uses a Beebo Relay or VPN route. UI should derive route from authenticated transport status from the backend, with an explicit `Home`, `Direct`, `Beebo Relay – [region]`, or `Beebo VPN – [region]` label. Verify on a genuinely different network; being on a friend’s Wi-Fi is not direct access to the user’s home computer.

### 5. Private server telemetry and regional expansion policy

Implemented disabled-by-default telemetry foundation:

- `worker/serverTelemetry.js`
- `worker/migrations/20260920_server_telemetry_v1.sql`
- `worker/SERVER-TELEMETRY.md`
- `worker/test/server-telemetry.test.mjs`
- `worker/worker.js` imports/routes
- `vpn/NETWORK-OBSERVABILITY-AND-REGIONAL-EXPANSION.md`

Design:

- Ingest endpoint: `POST /telemetry/v1/report`, signed HMAC.
- Feature is off until `BEEBO_SERVER_TELEMETRY_ENABLED=1`.
- Owner endpoint: `GET /owner/api/server-telemetry`.
- Records coarse region, capacity, active connections, current/average/peak bandwidth, p50/p95 latency and health timestamp only.
- Explicitly rejects IPs, exact GPS/coordinates, customer IDs, viewing history and other private identifiers.
- 35-day retention.

Private prototype:

- `D:\MovieAPP\beebotv\owner-operations\index.html`
- `owner-operations\PUBLIC-STATUS-PAGE-SPEC.md`
- `owner-operations\robots.txt`

Public page may show aggregate region health and maintenance. It must not show households, exact locations, viewer counts, IPs, revenue, or capacity details that aid abuse/targeting.

**Regional expansion policy:** paid household demand only. Exclude free at-home Beebo users entirely from revenue, capacity, demand and expansion calculations. Calculate true contribution after payment fees/refunds, network/egress, support/security/control-plane and tax/currency costs. Current proposed gate: at least 35% contribution margin, a three-month forecast, sensitivity check, 90-day demand/quality evidence, human approval, staged rollout and rollback. Do not auto-move customers merely because a threshold is crossed.

### 6. Website updates already made locally

Website root: `D:\MovieAPP\beebotv`.

- Entertainment `index.html`, `updates.html` and `polish.css` contain two-panel Windows/Android release status/download presentation using existing origin download routes.
- Domain sites `domain-sites/beeborelay.com/index.html`, `beebovpn.com/index.html`, `beebospace.com/index.html` have a matching warm cream two-panel release/download design.
- Product sites must honestly say “under construction” where there is no downloadable, configured product.
- `polish.css` and `polish.js` dynamically add an accessible gold/brown fixed centre `Top` button after scrolling.
- No site deployment occurred as part of this work.

### 7. Game and feature documentation

Created in `D:\MovieAPP\beebotv`:

- `GAME-CATALOG-INVENTORY.md` and `.json`: source-backed inventory of 43 implemented games (39 campsite, 4 solo).
- `GAME-PAGE-BUILD-PLAN.md`: individual game page architecture and screenshot requirements.
- `PUBLIC-FEATURE-CAPTURE-CATALOGUE.md`: public-safe, source-backed catalogue of desktop, Android, browser, privacy, setup, remote access, Official Free TV and games. It explicitly separates **Released**, **Implemented — capture required**, **Implemented — service launch required**, and **Planned / do not publish**.
- `BEEBO-SAMPLE-WALKTHROUGH-PLAYBOOK.md`: full sample-account recording/screenshot process.

**Important:** Do not fabricate screenshots. Use genuine current-build captures from the `BeeboSample` account. Promotional illustrations cannot be called app screenshots.

## Website requirements still to build

1. A public, anonymous competitor comparison page: refer to providers as `Service A`, `Service B`, and `Service C`; include “checked on” date and source methodology; use neutral evidence-based wording. Do not claim “lowest price” or “most features” without current, country-specific proof.
2. A private owner-only research page that identifies actual providers, source URLs, date checked, plan levels, regional/pricing caveats and feature evidence. Keep it out of the public web root and indexing.
3. Detailed Beebo feature pages with real approved screenshots, short clips, “what this button does,” availability state and limitations.
4. One public HTML page per finished game with the legal public name, a genuine screenshot, how-to-play, interaction/guest/bot availability and a playable browser demo only if that demo faithfully represents the game.
5. A safe public server status page. Keep the detailed capacity/traffic/revenue/geographic operations map owner-only.
6. Use current release metadata files for download version/date/time; never hand-type release data.

## Recording and screenshot plan

Use `BeeboSample` only. Record:

1. Website download panel → Windows installer → Beebo desktop launch.
2. Owner account creation → select sample folders → library scan.
3. Movies/TV, missing item, cast discovery, external search, playlists, upload history clear, users/privacy controls and log out.
4. Android APK download/install → safe sample sign-in → phone connection.
5. Android Movies/TV/missing episode/cast/player and **accurate** route banner.
6. Campsite temporary hotspot, guest join, photo/video group sharing with synchronized swipe, stories, 4-in-a-row, Sea Battle and other real game screens.
7. Watch Together only after it passes a two-current-device test. Do not claim browser guest video if it is not released.

Before publishing, redact every frame; remove personal library data, real QR codes, addresses, devices, Wi-Fi info and e-mail.

## Research and legal notes

### OVH network planning

Official sources reviewed:

- https://www.ovhcloud.com/en/vps/unmetered-vps/
- https://us.ovhcloud.com/bare-metal/

OVH “unmetered” does **not** mean unlimited performance. Plans have bandwidth ports/rates and product/location restrictions; APAC may have different caps/throttling and fair-use conditions can apply. Build service controls around measured capacity, CPU, RAM, disk I/O, latency, packet loss and headroom — not just total GB.

Use direct-first connections. Do not impose a monthly GB relay cap merely because relay use costs capacity, but protect the network with household concurrency, fair-share bandwidth policy, adaptive video quality, server headroom and workload isolation. Gaming, VPN and media relay workloads must have separate quotas/reservations or separate nodes so a game host cannot hurt streaming/VPN reliability.

The household/owner stats should show, without titles/destinations/history:

- At-home/LAN gigabytes
- Direct away-from-home gigabytes
- Beebo Relay gigabytes
- VPN upload/download gigabytes
- Current route, connected session time, bitrate, latency/buffer where accurate
- Daily, 7-day and 30-day totals

### Plex research (official sources)

- Plex Home: up to 15 members, which is a profile/member limit rather than a remote-stream guarantee: https://support.plex.tv/articles/203815766-what-is-plex-home/
- Plex bandwidth, per-user remote-stream and transcoding controls: https://support.plex.tv/articles/227715247-server-settings-bandwidth-and-transcoding-limits/
- Plex Relay has documented quality limitations (reference before comparing): https://support.plex.tv/articles/216766168-accessing-a-server-through-relay/
- Remote Watch Pass overview: https://support.plex.tv/articles/remote-watch-pass-overview/

Use primary/current official pricing pages at the time any public comparison is written. Pricing varies by country, currency, billing cycle and date.

### Trademark naming

Use original Beebo-branded descriptive names such as `Beebo 4-in-a-row`. A generic game name is not something Beebo can exclusively own. Before commercial branding/claims, search CIPO and obtain trademark-law advice:

- https://ised-isde.canada.ca/site/canadian-intellectual-property-office/en/trademarks/basic-search

## Recommended work order

1. Stabilize Android build environment with a compatible JDK 17 and resolve the Gradle lock. Run focused tests and full appropriate builds.
2. Review current dirty changes and commit only coherent, tested changes in small logical commits.
3. Finish/verify user login, account recovery, adult profile privacy, folder privacy and 6-person household enforcement.
4. Deploy a non-production test worker/relay/VPN environment. End-to-end test at home, another Wi-Fi, cellular, relay route and device/session cap.
5. Add strongly consistent household lease enforcement before more than one region exists.
6. Configure Stripe products/prices only after checkout, webhook signature verification, entitlements, cancellation/refund and customer messaging are fully tested.
7. Package and sign installers; publish only verified builds and exact release metadata.
8. Produce genuine sample captures, then build detailed website feature/game pages around those assets.
9. Build owner operations dashboard from real telemetry; keep public status aggregate and safe.
10. Only then assess Apple/Linux/TV clients and future hosting/rewards products against the stable API and account model.

## Definition of ready to advertise/sell

A service is ready only when it has all of: tested client, tested backend, verified entitlement/payment flow, privacy/security review, accurate customer wording, support/recovery flow, monitoring/alerts, documented limits, current website/download, current terms/privacy copy, and successful tests from real separate networks/devices.

## Current known blockers / “missing” list

- Real deployed relay/VPN infrastructure and multi-region central capacity store.
- Live Stripe products, webhooks, receipt/refund/cancellation testing and billing portal.
- Android build/test environment currently blocked by JDK mismatch and Gradle wrapper lock.
- Signed production Windows/Android releases incorporating the current source changes.
- Genuine screenshots/video clips for every desktop, Android and game feature.
- Public comparison page plus private evidence sheet.
- Complete password reset system and final private-folder cryptography/security review.
- Full server monitoring, alerting, incident process and capacity isolation.
- Legal review/terms/privacy/refund/support pages before sales.
- Any Apple/Linux/TV, managed hosting, game hosting, rewards/offers, global server expansion and licensed TV service are future work, not ready products.
