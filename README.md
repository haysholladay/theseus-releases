# Theseus — releases and update feed

This repository exists to serve **Theseus's in-plugin update check**. It holds no source.

Each release carries two assets:

| asset | purpose |
|---|---|
| `Theseus-<version>.pkg` | the signed, notarized macOS installer |
| `latest.json` | the feed the plugin reads |

Theseus requests exactly this URL:

```
https://github.com/haysholladay/theseus-releases/releases/latest/download/latest.json
```

`/releases/latest/` follows whichever release is marked **Latest**, so publishing a new
release switches the feed over; deleting one rolls it back.

## Requirements this repo must keep

- **Public.** The plugin fetches with no credentials — a private repo 404s for everyone.
- The asset must be named **exactly `latest.json`**, attached to the release marked Latest.
- `latest.json` must carry these four keys — the updater reads only these:

```json
{
  "version": "1.21",
  "notes":   "What changed, in one short paragraph.",
  "url":     "https://github.com/haysholladay/theseus-releases/releases/latest",
  "pkg":     "https://github.com/haysholladay/theseus-releases/releases/download/v1.21/Theseus-1.21.pkg"
}
```

`version` is compared against the running build; `pkg` is what the in-plugin
downloader fetches; `url` is the fallback opened in a browser when `pkg` is absent.

---
Kalide Systems™
