# Publishing an app to beebotv.com — runbook for a Cowork agent

You (the AI agent reading this) are updating **Nick's website** so a new or updated Android
app can be downloaded from it. Follow these steps exactly. The human's only manual step is the
final `git push` — everything before that is yours to do.

## The setup (facts you need)

- **Live site:** https://beebotv.com (GitHub Pages, custom domain via the `CNAME` file — never
  delete or change `CNAME`).
- **GitHub repo:** `https://github.com/SWGfan/beebotv.git`, branch **`main`**.
- **Local folder on the PC:** `D:\MovieAPP\beebotv` (reachable via your device tools; inside
  `device_bash` it's usually under `$HOME/mnt/` by the folder name, e.g. `$HOME/mnt/beebotv`).
- **Where APKs live:** `downloads/` in that repo. Files are named `<AppName>-v<version>.apk`,
  e.g. `BeeboEntertainment-v2.1.apk`, `BeeboMirror-v2.2.apk`, `BeeboAuto-v2.0.apk`.
- **The page people download from:** `index.html`, in the "Get the app" section.

## What you must already have

A **built, signed release APK** for the app being published. This runbook only covers putting an
existing APK on the website — it does NOT build the app. If you don't have the APK, get it from
Nick or from wherever that project's build produces it, then continue.

Important for **updates to an existing app**: the new APK must be signed with the **same signing
key** as the previous version, or phones won't install it over the old one (Android rejects a
signature change). A brand-new, separate app is its own app with its own key — that's fine.

## Steps

### 1. Put the APK in `downloads/`

Copy the release APK into `D:\MovieAPP\beebotv\downloads\` using the naming convention
`<AppName>-v<version>.apk` (match the existing style — PascalCase app name, `-v`, dotted version).

**Do not delete or overwrite older APKs.** Leave them in place so old links keep working; just add
the new one. (If you have the APK as a file you produced, write it there; if a human is providing
it, tell them the exact filename and folder to drop it in.)

Note the file's size in MB — you'll put it in the label in step 2.

### 2. Edit `index.html`

Open `index.html` and find the "Get the app" section (search for `Get the app` and
`downloads/`). It looks like this:

```html
<a class="btn btn-primary btn-lg" href="downloads/BeeboEntertainment-v2.1.apk" download>⬇ Download Beebo Entertainment</a>
<p style="color:var(--muted);font-size:.9rem;margin-top:12px">v2.1 · Android APK · ~17 MB · for arm64 phones</p>
<p style="color:var(--muted);font-size:.95rem;margin-top:14px">Car companions (Android):
  <a href="downloads/BeeboAuto-v2.0.apk" download>⬇ Beebo Auto</a> &nbsp;·&nbsp;
  <a href="downloads/BeeboMirror-v2.2.apk" download>⬇ Beebo Mirror</a>
</p>
```

Then, depending on what you're publishing:

- **Updating the MAIN app (Beebo Entertainment):** change the main button's `href` to the new
  filename, and update the version + size in the grey label line (`v2.1 · Android APK · ~17 MB …`).
  Then update the **"What's new in vX.X"** box just below it: change the heading version and
  rewrite the bullet list to describe this release in plain, friendly language (what the user
  gets, not internal detail). Keep it to 2–4 short bullets.

- **Updating a companion (Beebo Auto / Beebo Mirror):** just change that companion's `href` to the
  new filename in the "Car companions" line.

- **Adding a BRAND-NEW app:** add a new `<a ... download>` link. If it's a companion-style extra,
  add it to the "Car companions" line next to the others. If it deserves its own prominence, add a
  new labelled button block modeled on the main one. Match the existing classes and inline styles
  so it looks native to the page. Give it a short label line (version · Android APK · ~size ·
  for arm64 phones).

Keep every edit consistent with the surrounding markup — same classes, same style attributes,
same emoji (`⬇`). Don't restyle the page.

### 3. Sanity-check before committing

- The `href` filename matches a file that actually exists in `downloads/` (exact case).
- The version number and size in the label match the new APK.
- You didn't touch `CNAME`, and didn't delete old APKs.
- The HTML still looks well-formed (no unclosed tags around your edit).

### 4. Commit (you), then push (Nick)

From the repo folder, stage and commit — but **do not push**. Pushing is Nick's step.

```bash
cd "$HOME/mnt/beebotv"          # the D:\MovieAPP\beebotv folder
git add -A
git commit -m "Publish <AppName> v<version>"
```

Then tell Nick, in plain words:

> Done — I've committed the <AppName> v<version> update to the website. Run `git push` from the
> `beebotv` folder on your PC and it'll go live at beebotv.com in about a minute.

If Nick's `git commit`/`git push` ever fails with a `.git/index.lock` or similar lock error
(common on Windows), the fix is to delete the stale lock and retry:

```
del /s /q .git\*.lock
git push
```

### 5. After Nick pushes

GitHub Pages redeploys within ~1 minute. Nick can then open **beebotv.com** on his phone, tap the
download for the app, and install it. (Android will warn it's from outside the Play Store — that's
expected for a direct install.) If the download 404s, the `href` filename didn't match the file in
`downloads/` — fix the name and repeat.

## Guardrails (do not skip)

- **Never delete `CNAME`** — it's what points beebotv.com at the site.
- **Never delete old APKs** in `downloads/` — old links and older phones may still use them.
- **Don't push** — only Nick pushes.
- **Same-key signing** for updates of an existing app, or it won't install over the old one.
- Only touch what the task needs — the download link, its label, and the "What's new" box. Leave
  the rest of the site alone.

## Note (separate from the website)

The main Beebo app also has an **in-app updater** that is NOT the website — it's served by Nick's
home desktop program from a `version.json` next to the APK. That's a different channel; this
runbook is only about the public website download. Don't try to wire the two together unless Nick
asks.
