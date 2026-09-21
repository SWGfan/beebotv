# Beebo Game Pages — Build Plan

## Purpose

Create one public, accessible HTML page for every **built** Beebo game, plus a Games index. Each page must use an actual capture from the current app build, explain the real play mode, and offer a small browser demo only where it faithfully represents the shipped game. Do not use emulator, ROM, console, or third-party game language or imagery.

This plan covers the 39 Campsite games and four solo games found in the mobile source: **43 games total**. `Drop Four` is the public name for the drop-and-line game. Do not use `Drop Four` in page titles, descriptions, image filenames, metadata, or UI.

## What can be used today

| Asset | What it is | Safe use | Not suitable for |
|---|---|---|---|
| `assets/Drop Four-guests.png` (390×1069) | Real phone capture of Drop Four with guests | Drop Four page, guest-play explanation | A general game-library hero or a bot-play claim |
| `assets/guest-games-menu.png` (390×1409) | Real phone capture of the guest Games menu | Games index and guest-play explainer | A screenshot for a specific game |
| `assets/game-update-1.35/Drop Four.svg` | Promotional illustration | Drop Four card accent | A claimed app screenshot |
| `assets/game-update-1.35/chess.svg` | Promotional illustration | Chess card accent | A claimed app screenshot |
| `assets/game-update-1.35/fivedice.svg` | Promotional illustration | Five Dice card accent | A claimed app screenshot |
| `assets/campsite.png`, `assets/camp-morning.png`, `assets/friends-campsite.png` | Campsite marketing artwork | Shared Campsite introduction | Individual-game UI proof |

There are **no existing actual captures** for Sea Battle or the other 41 games. The page generator must therefore show a capture-required state in development and must not publish a page with a fake screenshot.

## Page structure and filenames

```
games.html                         # searchable index; group by play type
games/four-in-a-row.html
games/sea-battle.html
games/<slug>.html                  # one page per game below
assets/games/<slug>/hero.webp      # real phone capture, 1440×900 or larger
assets/games/<slug>/setup.webp     # real setup / lobby capture
assets/games/<slug>/play.webp      # real in-play capture
assets/games/<slug>/result.webp    # optional real result capture
assets/games/<slug>/bot.webp       # only when the shipped game truly supports it
assets/games/<slug>/guest.webp     # only when guests are part of its real flow
```

Use lossless PNG during capture review, then produce WebP from the approved capture. Keep the original source capture outside the public web root. Give every image accurate alt text, such as: `Drop Four on a phone showing red and gold counters and the current-player prompt.`

## Universal page template

Every `games/<slug>.html` page should contain the following, in this order:

1. Breadcrumb: `Beebo Entertainment / Games / <game name>`.
2. Page title, concise original description, age/attention guidance, and truthful play badges: `Solo`, `Play against Beebo`, `Guest phones`, `2–12 players`, `Works in Campsite Mode`, or `Offline on the host phone`.
3. A real in-app screenshot in a responsive `<figure>` with a specific `alt`; no image is marked as a screenshot unless it came from the app.
4. “How to play” in three to five numbered steps based on actual controls.
5. “Choose your way to play” panel: `Play against Beebo`, `Play with guests`, or `Requires guests`, as appropriate.
6. Optional small **browser preview**, clearly labelled `Preview of the game idea — sign in to Beebo to play with your room`. A preview is never a replacement for the product and must have no tracking, sign-in, ads, or arbitrary remote code.
7. A capture gallery for setup, play, and result states once actual images exist.
8. Accessibility and safety notes: touch targets at least 44×44 CSS pixels, no time-based flashing, no forced sound, keyboard-visible focus, high-contrast labels, and no data collection in the preview.
9. Download panels for Windows and Android, reusing the verified release/version data already used by the main site.
10. Footer links to Beebo Entertainment, Beebo Relay, Beebo VPN, and Beebo Space.

Reusable skeleton:

```html
<main id="main-content" class="game-page">
  <nav aria-label="Breadcrumb"><a href="../games.html">Games</a> / <span aria-current="page">Drop Four</span></nav>
  <section class="game-hero">
    <div>
      <p class="eyebrow">Campsite game</p>
      <h1>Drop Four</h1>
      <p>Take turns dropping counters. Make a line of four before your opponent does.</p>
      <ul class="game-badges" aria-label="How this game plays">
        <li>2 players</li><li>Play against Beebo</li><li>Guest phones supported</li>
      </ul>
      <a class="button" href="../app-on-your-phone.html">Get the Beebo app</a>
    </div>
    <figure>
      <img src="../assets/games/four-in-a-row/play.webp" width="1440" height="900"
           alt="Drop Four in Beebo showing the game board and the active player's turn.">
      <figcaption>Actual Beebo mobile game screen.</figcaption>
    </figure>
  </section>
  <section aria-labelledby="how-to-play"><h2 id="how-to-play">How to play</h2><ol><!-- game-specific real steps --></ol></section>
  <section aria-labelledby="preview-title" class="game-preview">
    <h2 id="preview-title">Try the game idea</h2>
    <p>This short preview is for learning the rules. Use Beebo to play with your guests.</p>
    <div id="game-preview-root" data-game="four-in-a-row"></div>
  </section>
  <section class="downloads" aria-label="Download Beebo"><!-- Windows and Android release panels --></section>
</main>
```

The generated template must not place untrusted player names or game text into `innerHTML`; use `textContent`. Each preview must be isolated to a per-page ES module, have no network calls, and clean up timers when reset or unloaded.

## Built-game capture and preview matrix

### Board and strategy

| Public page title | Slug | Real capture set required | Browser bot preview | Guest-play wording |
|---|---|---|---|---|
| Drop Four | `four-in-a-row` | setup, mid-game, win | Yes; a simple, original four-counter demo that mirrors the shipped rules | Two people can play from their own phones; host can also play Beebo |
| Tic-Tac-Toe | `tic-tac-toe` | board, result | Yes | Two guest phones or Beebo opponent |
| Checkers | `checkers` | board, forced capture or result | Yes | Two guest phones or Beebo opponent |
| Reversi | `reversi` | board, score result | Yes | Two guest phones or Beebo opponent |
| Nine Men’s Morris | `nine-mens-morris` | placement, movement, result | Yes | Two guest phones or Beebo opponent |
| Sea Battle | `sea-battle` | ship placement, attack grid, result | Yes only after the browser version includes drag/drop placement and does not expose the opponent board | Two guest phones or Beebo opponent |
| Dominoes | `dominoes` | hand, board line, result | Yes | Two to four guest phones or Beebo opponents |
| Snakes and Ladders | `snakes-and-ladders` | board, on-board dice roll, result | Yes; use an original board design | Guest phones or Beebo opponents |
| Ludo | `ludo` | board, on-board dice roll, result | Yes; use an original board design | Guest phones or Beebo opponents |
| Dots and Boxes | `dots-and-boxes` | in-play grid, claimed boxes, result | Yes | Two guest phones or Beebo opponent |
| Mancala | `mancala` | turn, capture, result | Yes | Two guest phones or Beebo opponent |
| Five Dice | `five-dice` | on-board 3D dice roll, held dice, scorecard | Yes; use the same original scoring vocabulary as the app | Guest phones or Beebo opponents |
| Chess | `chess` | board, level selector, result | Yes only if it uses a complete legal-move engine; otherwise show a non-playable rules explorer | Two guest phones or Beebo opponent at three shipped levels |

### Cards, matching and chance

| Public page title | Slug | Real capture set required | Browser bot preview | Guest-play wording |
|---|---|---|---|---|
| Go Fish | `go-fish` | private hand, request, result | Yes | Two to four guest phones or Beebo opponents |
| Crazy Eights | `crazy-eights` | hand, suit choice, result | Yes | Two to four guest phones or Beebo opponents |
| Old Maid | `old-maid` | hand, draw, result | Yes | Two to four guest phones or Beebo opponents |
| Snap | `snap` | card pile, call action, result | Yes | Two guest phones or Beebo opponent |
| War | `war` | deal, comparison, result | Yes | Two guest phones or Beebo opponent; no ranked claim |
| Pairs | `pairs` | face-down grid, match, result | Yes | Two guest phones or Beebo opponent |

### Outdoor, quiz and talk

| Public page title | Slug | Real capture set required | Browser bot preview | Guest-play wording |
|---|---|---|---|---|
| Movie Trivia | `movie-trivia` | question, answer reveal, score result | Yes, using only Beebo-authored or licensed questions | Guest phones or Beebo opponent |
| Rock Paper Scissors | `rock-paper-scissors` | choice, reveal, round result | Yes | Guest phones or Beebo opponent |
| Sight Race | `i-spy` | prompt, answer/reveal, result | Yes | Guest phones or Beebo prompt player |
| Car Bingo | `car-bingo` | card, marked line, win | Yes | Guest phones or Beebo opponent |
| Nature Bingo | `nature-bingo` | card, marked line, win | Yes | Guest phones or Beebo opponent |
| Story Builder | `story-builder` | prompt, contribution, finished story | Yes | Guest phones or Beebo co-writer |
| Category Chains | `category-chains` | prompt, turn list, result | Yes | Guest phones or Beebo co-writer |
| Campfire Stories | `campfire-stories` | opening prompt, contribution, finished story | Yes | Guest phones or Beebo co-writer |
| Hot Potato | `hot-potato` | turn, pass, result | Yes | Guest phones or Beebo opponent |
| Classic Bingo | `classic-bingo` | caller, card, valid bingo | Yes | Guest phones or Beebo callers |

### Games that genuinely require guests

These pages may have an interactive **rules teaser** (select a sample answer, draw a local line, or reveal an example state), but must not advertise “play against Beebo” or a bot match. Their page CTA is `Start Campsite Mode and invite your guests`.

| Public page title | Slug | Real capture set required | Why no bot preview |
|---|---|---|---|
| This or That | `this-or-that` | question, individual votes, room result | The point is the real room split |
| Tough Choices | `would-you-rather` | question, individual votes, room result | The point is the real room split |
| Twenty Questions | `twenty-questions` | secret prompt, question, result | Requires a human’s secret and responses |
| The Quiet Game | `the-quiet-game` | group start, timer/status, result | Requires a real group maintaining quiet |
| Pick the Next One | `pick-the-next-one` | prompt, selections, result | Requires room choice |
| Who’s the Spy? | `whos-the-spy` | private role, clue round, vote | Secret social roles need real participants |
| Campfire Werewolf | `campfire-werewolf` | private role, night action, village vote | Secret social roles need real participants |
| Sketch & Guess | `sketch-and-guess` | drawing, guesses, reveal | Drawing and guessing need real people |
| Fake Out | `fake-out` | prompt, entries, vote, reveal | Bluffs need real participant entries |
| Two Truths and a Lie | `two-truths-and-a-lie` | entry editor, votes, reveal | Personal statements need real participants |

### Solo games

| Public page title | Slug | Real capture set required | Browser preview |
|---|---|---|---|
| Five Letters | `five-letters` | daily board, keyboard, result | Yes; a limited original word puzzle with an explicit word list licence/review |
| Number Grid | `sudoku` | board, note mode, completion | Yes |
| Hidden Mines | `minesweeper` | board, flag, result | Yes |
| Patience | `solitaire` | tableau, foundation move, win | Yes; traditional card rules, original card art |

## Capture runbook

1. Use the current signed-in sample account and the current release build, with only Beebo-owned sample data visible.
2. Put the phone at native portrait resolution. Capture the full screen with the status bar hidden or scrubbed of personal information.
3. For each game, capture: game card/menu, setup or lobby, meaningful in-play state, and outcome. Capture guest-only games on at least two guest devices when showing the room flow.
4. For Sea Battle, capture ship drag/drop placement, a legal shot, hit/miss feedback, and a result. Do not capture a screen that exposes both players’ private ship positions.
5. For dice games, capture the 3D die while visibly rolling on the board and one settled result; no still image may imply animation by itself.
6. Review each capture for personal library items, e-mail addresses, Wi-Fi names, QR codes, passwords, tokens, exact location, or copyrighted media artwork. Recreate a Beebo-only sample scene if any appear.
7. Use a capture manifest (`assets/games/captures.json`) recording game slug, build version, capture date, device, source screen, alt text, and approval status.
8. Publish only captures marked `approved`. The index card should show a neutral Beebo-made illustration or `Coming soon` state until then.

## Implementation order

1. Build `games.html`, shared CSS, shared header/footer, and the page generator with the template above.
2. Publish the three pages that have supporting assets today only after replacing the promotional artwork with approved real captures: Drop Four, Chess, and Five Dice. The existing SVGs can remain decorative, never labelled as screenshots.
3. Capture the showcase priority set: Drop Four, Sea Battle, Five Dice, Movie Trivia, Chess, Campfire Werewolf, Sketch & Guess, Story Builder, Five Letters, and Patience.
4. Add the remaining pages in groups after their captures are approved.
5. Add lightweight browser previews only after the game-specific rules and screenshots are approved. Do not embed the Android app, a third-party game, an emulator, or a remote iframe.
6. Add the Games index to all Beebo company sites using the same cream/white/gold visual system and download panels; product sites may link to the Beebo games index rather than duplicate all 43 pages.

## Naming and marketing guardrails

- Use `Drop Four`, never `Drop Four` or `Drop Four`.
- Use `Sea Battle`, never `Battleship`.
- Use `Reversi`, not `Othello`; `Crazy Eights`, not `UNO`; `Pairs`, not `Memory`; and `Snakes and Ladders`, not `Chutes and Ladders`.
- Do not use any emulator, ROM, N64, PS2, console, or game-library claim.
- Do not claim a browser preview is the installed Beebo product.
- The existing source licensing document is a useful product naming reference, but legal counsel should review names, art, marketing, and regional availability before commercial launch.

## Acceptance checks

- Every listed page has a unique title, canonical URL, description, and Open Graph image based on an approved Beebo capture.
- No page calls a promotional illustration a screenshot.
- No guest-required page advertises bot play.
- Every bot preview reflects a feature currently present in the shipped app.
- Drop Four and Sea Battle use only the safe names everywhere, including URLs and image alt text.
- All preview controls work by keyboard and touch; focus order and contrast are verified on phone and desktop sizes.
- All download panels read release version/date/time from the shared release data rather than hand-entered text.
