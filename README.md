# hanabifinder-data

Static event-data feed for the [Hanabi Finder](https://apps.apple.com/jp/app/id6792519666) iOS app, served via GitHub Pages.

`events.json` is the live feed the app fetches at `https://relsirc.github.io/hanabifinder-data/events.json`. Format:

```json
{
  "version": 1,
  "updatedAt": "2026-08-23T00:05:09Z",
  "events": [ ... ]
}
```

The app only accepts a fetched file if `version` is strictly greater than what it already has cached — so every publish must bump `version`.

## Publishing an update

Don't hand-edit `events.json` here. From the main `hanabifinder` repo, edit `hanabifinder/Resources/FireworkEvents.json`, then run:

```
swift Scripts/PublishEvents.swift
```

This pulls this repo, bumps `version` (current + 1, or pass an explicit version as an argument), writes the new `events.json` here, commits, and pushes. It also rewrites the main repo's bundled `FireworkEvents.json` with the same version so the next app build ships a matching baseline.
