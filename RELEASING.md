# Publishing Beebo updates

The public footer and homepage download area display versions and Eastern dates/times from the update feeds. Keep these feeds accurate whenever a build is published.

- `desktop-version.json`: version, a versioned installer URL, SHA-256, notes, and `publishedAtUtc` from the actual GitHub release publication time.
- `downloads/app-build.json`: versionName, versionCode, bytes, SHA-256, builtAtUtc and (when published) publishedAtUtc. UTC timestamps must include a timezone. The website converts them to Eastern time.
- If an Android build only has a build timestamp, the page labels it Built. A publication timestamp is labelled Released. Do not invent a release time or copy one from an older build.
- `polish.js` refreshes the labels from these feeds, so new releases do not require rewriting every HTML page. Embedded labels are the last published fallback if metadata cannot be fetched.
- If the Windows feed has no timestamp, the page attempts to read it from the matching `Beebo-<version>` GitHub release. Do not rely on that fallback for normal publishing.

Build and test first. Keep Android signing compatible with the existing website APK. Upload and verify the versioned Windows release before pointing the feed at it. Push the website, then verify its live metadata and Android APK hash. Set the verified release as latest for the homepage Windows download link. Keep rollback copies in a private archive, outside the public website and public release assets. Only current supported installers may be downloadable. Nick requested this policy on September 20, 2026 because older builds may bypass licensing.
