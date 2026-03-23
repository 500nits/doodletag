# DoodleTag Static Site Bundle

Copy this folder to the static website root so these deploy paths exist:

- `/.well-known/assetlinks.json`
- `/m/index.html`

## What this bundle does

- `/.well-known/assetlinks.json`
  - enables Android App Links verification for `https://doodletag.500nits.com/m/...`
- `/m/index.html`
  - supports backend-free shared links in the form:
  - `https://doodletag.500nits.com/m/?dtag=<encoded-https-dtag-url>`

## Important values

- Android package name in the app code:
  - `com.u500nits.DoodleTag`
- Release keystore SHA-256 used in this bundle:
  - `27:AB:F8:AA:45:46:FB:D4:9B:26:FC:07:32:1E:56:21:67:11:8B:86:6D:EE:40:B5:1C:5A:22:AC:99:EF:7E:08`

If Google Play App Signing is enabled, replace the fingerprint in `.well-known/assetlinks.json` with the Play Console
app-signing SHA-256 fingerprint before deploying.

## Static-site sharing model

This bundle assumes there is no backend lookup for `/m/<id>`.

Use links like this instead:

`https://doodletag.500nits.com/m/?dtag=https%3A%2F%2Fdoodletag.500nits.com%2Ffiles%2Fabc123.dtag`

The Android app already accepts links when either:

- the URL path itself ends in `.dtag`, or
- the URL contains `?dtag=https://...something.dtag`

## Optional edits before deploy

Inside `m/index.html`, fill these constants if you want automatic store fallback:

- `ANDROID_STORE_URL`
- `IOS_STORE_URL`

If you leave them empty, the page will still:

- try to reopen the app link once,
- expose a direct `.dtag` file button,
- avoid guessing any store URLs.
