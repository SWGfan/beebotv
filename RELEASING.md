# Publishing Beebo updates

Public labels and download links follow `desktop-version.json` and `downloads/app-build.json`. Keep version, SHA-256, size, notes and publication time accurate. Store UTC timestamps with a timezone; the website displays Eastern time with seconds. Build time and publication time are different fields.

## Hosting

Current installers live at `https://origin.beebo.tv/downloads/` on OVH in `/srv/beebo-public/downloads/`. Publish only the current supported version for each product. Keep old installers and hashes privately, outside the public directory. Do not add binaries to this public Git repository or create another GitHub release.

The website itself currently uses GitHub Pages. That migration is separate; do not make its repository private while Pages is serving it. Old files may still exist in public Git history until that migration is complete.

## Release checks

1. Build and test. Check Android signing compatibility; report Windows code-signing status accurately.
2. Back up the old artifact privately and upload the new versioned artifact to OVH. Check its SHA-256 and byte count on the server.
3. Set `publishedAtUtc` to the actual time the new file became publicly available. Update both metadata feeds, embedded version/date fallbacks, release notes and download links. Never reuse an older release date.
4. Replace the legacy Windows download bucket object with the same installer, using the service copy tool. Verify the copy actually ran and its hash matches.
5. Test live downloads, range requests, metadata and the rendered pages. Publish the website and verify the deployment.
6. Withdraw superseded public artifacts after the new version works. Keep rollback copies privately. Removing a download cannot revoke copies already installed or shared.

`polish.js` refreshes release labels and supported OVH download links. Embedded links and labels remain usable if a metadata request fails. Do not publish credentials, signing keys, or private backup directories.
