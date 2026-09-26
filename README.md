# Handwritten to Markdown releases

This repository hosts the Sparkle appcast at `appcast.xml`. Installable app ZIPs
are attached to GitHub Releases, not committed to Git.

The source repository's `scripts/publish_release.sh` signs the update archive,
uploads it here, and advances the appcast. Each app build number must increase.
