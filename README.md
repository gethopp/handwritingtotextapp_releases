# Handwriting to Text releases

This repository hosts public stable releases of Handwriting to Text. Each
release includes a notarized installer DMG, an EdDSA-signed Sparkle update ZIP,
and `appcast.xml` as a release asset. The installer is always named
`HandwritingToText.dmg`; ZIP names and release tags remain versioned.

The app reads the latest stable release feed from:

https://github.com/gethopp/handwritingtotextapp_releases/releases/latest/download/appcast.xml

The website uses the stable installer link:

https://github.com/gethopp/handwritingtotextapp_releases/releases/latest/download/HandwritingToText.dmg

## Future releases

Build and publish from the source repository, following its
[release instructions](https://github.com/gethopp/handwrittingtotextkit/blob/main/docs/releasing.md).

1. Increment the app build number in both configurations and validate the source changes.
2. Configure the local `.env.release`, Developer ID certificate, Apple notary
   profile, GitHub CLI authentication, and matching Sparkle private key.
3. Run `bash scripts/build_release.sh` to build, sign, notarize, and staple
   the app and DMG.
4. Run `scripts/publish_release.sh` with the packaged app, notarized DMG,
   and Sparkle bin directory as arguments. It generates a fresh appcast,
   uploads all three assets to a draft, then publishes it and marks it latest.
5. Verify the release assets and the latest feed URL.

Never commit `appcast.xml` to this repository; upload it as a release asset
only. Release titles must be `Handwriting to Text <version>` (for example,
`Handwriting to Text 0.1`). Never append a parenthesized build number such as
`(1)` to a release title. Build numbers remain in tags and Sparkle metadata.
Keep the private signing key and credentials outside Git. The latest feed
URL is for stable releases; prereleases need a separate update channel.

## Existing installations

The original `v0.1-1` app reads the old raw GitHub feed URL. The committed
feed has been removed; the matching appcast remains attached to that release.
Those installations need a manual download of the next release containing
the new feed URL to resume automatic updates. Do not recreate the committed
feed. Keep the published DMG and ZIP unchanged.
