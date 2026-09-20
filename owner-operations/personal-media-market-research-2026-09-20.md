# Personal-media market research — internal working sheet

**Research date:** 20 September 2026 (America/Toronto)  
**Scope:** personal media products relevant to Beebo Entertainment.  
**Use:** internal product and pricing research only. This file is not customer-facing. It is a factual snapshot, not legal advice and not a claim about a competitor's service in every country.

## How to use this sheet

Prices, availability, feature sets, app support, and remote-access rules change. Check the linked primary source immediately before using any number in a public campaign, checkout, sales call, or comparison. Prices below are explicitly labelled with the source currency. A Canadian price, tax treatment, app-store price, and regional catalogue can differ from the stated USD website price.

## Snapshot table

| Product | Plan/pricing snapshot from its official source | Local and remote access | Household / user policy | Relay / connection model | Official app/platform evidence | Relevant capabilities |
|---|---|---|---|---|---|---|
| Plex | Remote Watch Pass: **US$2.99/month** or **US$29.99/year** after its introductory period; prices outside USD may vary. Plex Pass is separate; the plan page must be rechecked for current price. | Local-network personal-media streaming is free. Remote personal-video playback requires a Remote Watch Pass or Plex Pass, subject to Plex's published rules. | Plex Home supports up to 15 members. That is a membership/profile rule; it is not a published promise of 15 simultaneous remote streams. Server owners have bandwidth and transcoding controls. | Plex's free live TV catalogue is separate from a user's media server. Do not describe it as a customer's self-hosted relay. | Plex says its personal media is available across supported devices; check current platform availability at release time. | Hardware transcoding, downloads, skip intro/credits, and remote streaming appear on Plex's plan comparison. |
| Jellyfin | No subscription is required for the official server or official clients. | Self-hosted local streaming. Remote access needs an administrator-controlled exposure method; Jellyfin documents port forwarding, reverse proxy, VPN, or a VPS reverse proxy. | Per-user remote access controls exist; its public docs do not present a household subscription plan. | No managed commercial relay described in the cited official networking documentation. The operator provides the connection method. | Official clients list includes Android, iOS/iPadOS, Android TV/Fire TV, Roku, WebOS, Samsung Tizen, Xbox, desktop and browser support. | Library, direct play/direct stream/transcoding depending on client and server hardware. |
| Emby | Premiere is sold as monthly, annual, or lifetime subscriptions. The official terms page does not state a price, so do not publish a number from this sheet. | User management and Emby Connect are listed as free; concurrent video-session limits are listed as Premiere. | Unless otherwise stated, Premiere is limited to 30 premiere devices per key; this is a device rule, not a concurrency promise. | No managed relay claim made here. | Official documentation lists iOS/iPadOS, Android, Android TV, Fire TV, Xbox/Windows, browser and several TV platforms, with feature differences by app. | Hardware-accelerated transcoding, live TV/DVR, downloads/sync, parental controls, concurrency limits and plugin-related features are in its feature matrix. |

## Primary sources

### Plex
1. [Plex plans](https://www.plex.tv/plans/) — retrieved 2026-09-20. States USD Remote Watch Pass standard pricing of US$2.99/month and US$29.99/year after the stated introductory period; says other currencies may vary; describes local free use and premium feature comparison.
2. [Plex 2025 remote-playback update](https://www.plex.tv/de/blog/important-2025-plex-updates/) — retrieved 2026-09-20. Explains remote personal-media playback policy and the relationship between a server owner's Plex Pass and users sharing that server.
3. [What is Plex Home?](https://support.plex.tv/articles/203815766-what-is-plex-home/) — must be rechecked before public use; source for the 15-member profile limit.
4. [Plex bandwidth and transcoding limits](https://support.plex.tv/articles/227715247-server-settings-bandwidth-and-transcoding-limits/) — must be rechecked before public use; source for owner-controlled remote/bandwidth behaviour.
5. [Plex free live TV overview](https://support.plex.tv/articles/free-live-tv-streaming-overview/) — describes a separately offered, licensed live-TV catalogue rather than a customer's personal server.

### Jellyfin
1. [Jellyfin clients](https://jellyfin.org/clients/) — retrieved 2026-09-20. Says no subscription is required for the server or official clients; lists official client platforms.
2. [Jellyfin networking](https://jellyfin.org/docs/general/post-install/networking/) — retrieved 2026-09-20. Documents local discovery, external access options, per-user external-access controls, and warns that exposing a port directly is not recommended.
3. [Jellyfin introduction](https://jellyfin.org/docs/) — retrieved 2026-09-20. Describes Jellyfin as a free-software media system.
4. [Jellyfin hardware selection](https://jellyfin.org/docs/general/administration/hardware-selection/) — retrieved 2026-09-20. Uses 20 Mbps upload as a remote-access starting point and recommends a 70% bandwidth cap when total upload is below 100 Mbps.

### Emby
1. [Emby Premiere terms](https://docs.emby.media/premiereterms.html) — retrieved 2026-09-20. Covers monthly/annual/lifetime terms and the 30-device default rule.
2. [Emby Premiere feature matrix](https://support.emby.media/support/articles/Premiere-Feature-Matrix.html) — retrieved 2026-09-20. Lists free versus Premiere capabilities by platform, including concurrent video-playback limits, remote login, live TV/DVR, hardware transcoding and downloads.

## Safe public-comparison rules
1. Do not use competitor names, logos, screenshots, app artwork, product copy, or price figures on the public anonymous page.
2. Do not say Beebo is "cheapest", "best", "more features", or "better value" unless a dated, country-specific, like-for-like, legally reviewed study supports that exact claim.
3. Do not state or imply that an alternative lacks a feature unless that claim is tied to a dated official primary source and a clearly defined plan/region.
4. Do not compare a Beebo **planned** feature against a competitor's shipping feature. Label Beebo items as **available**, **pilot**, or **planned** accurately.
5. Explain that an individual user's home upload speed, devices, and file formats determine actual remote-stream quality. A subscription price does not make a home server faster.
6. Put a visible review date, currency/territory caveat, and methodology link on each public comparison page. Archive screenshots/PDFs of sources internally before campaigns go live.

## Recommended Beebo comparison position (safe wording)
"Beebo is building a household-first personal-media experience. It keeps at-home viewing local, gives the owner practical household controls, and offers a paid away-from-home option with clear connection-status information. Features and availability vary by release, device, region and home connection."

This describes Beebo's intended product direction without ranking it against named products or promising outcomes not yet shipped.

