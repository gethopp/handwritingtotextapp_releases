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

Normal releases require no appcast commit or push to this repository.
Keep the private signing key and credentials outside Git. The latest feed
URL is for stable releases; prereleases need a separate update channel.

## Existing installations

The original `v0.1-1` app reads the committed `appcast.xml` through its raw
GitHub URL. Its matching appcast is also attached to that release. Preserve
the committed file so existing installations can still check for updates.

When the next release ships with the new feed URL and a higher build number,
copy that release's attached appcast into the legacy committed file and
commit/push it once. That migration update lets old installations upgrade to
the release-asset feed. Subsequent normal releases only upload assets.
