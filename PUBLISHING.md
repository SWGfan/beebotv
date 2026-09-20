# Publishing Beebo downloads

Follow `RELEASING.md` for metadata, dates, signatures and verification.

## Current-download-only policy

Nick requested on September 20, 2026 that older installers no longer be available publicly because older builds may bypass licensing. This replaces the previous instruction to retain older APKs in the public downloads directory.

- Publish only the current supported installer for each product.
- Keep older installers, their hashes and release notes in a private backup location, outside the public website and public repository history.
- Before replacing a current installer, verify the replacement's version, signature and hash and preserve a private rollback copy.
- Remove or privately archive the superseded public release asset and update all public download links. A hidden link alone does not revoke a downloadable file.
- Do not recreate old versioned APKs in this public repository during publishing.
- Until the website has moved to OVH, old APKs can still exist in this repository's public Git history. Removing them from the current branch does not erase that history. Complete the hosting migration and make the repository private to close that access route; do not make it private while GitHub Pages is still serving the live website.
- Do not promise that withdrawing downloads disables copies already installed or distributed elsewhere. Server-side entitlements and a compatible client update policy are separate controls.

## Release workflow

1. Build and verify the APK or installer, including compatible signing.
2. Save the previous artifact privately, then stage the new artifact and accurate update metadata.
3. Update the current download links and notes. Preserve the website domain configuration.
4. Publish only to the destination authorized by Nick. Current direction is to migrate Beebo hosting and repositories to OVH; do not assume permission for an unrelated new GitHub release.
5. Verify the live download, signature/hash metadata and the old public URL's unavailability.

Avoid publishing signing keys, account secrets or private backup directories.
