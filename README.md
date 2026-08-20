# Design Leaders Finland

We make small, focused apps that respect your privacy. No tracking. No ads. Each app costs 1 EUR.

## Apps

| App                                                                        | Description                                                                                        | App Store      | Google Play      | Web                                                    |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------- | ---------------- | ------------------------------------------------------ |
| [color-surface](https://github.com/Design-Leaders-Finland/color-surface)   | A living canvas that generates ever-changing abstract art from moon phase, device motion, and time | [App Store](#) | [Google Play](#) | —                                                      |
| [naoentendonada](https://github.com/Design-Leaders-Finland/naoentendonada) | English/Finnish → Brazilian Portuguese translator with speech input and word-by-word TTS           | [App Store](#) | [Google Play](#) | —                                                      |
| [wall](https://github.com/Design-Leaders-Finland/wall)                     | Anonymous public message board — 160 chars, 5-minute lifetime, no accounts                         | —              | —                | [wall.designleaders.fi](https://wall.designleaders.fi) |
| [ok-timelapse](https://github.com/Design-Leaders-Finland/ok-timelapse)     | Timelapse recording app for mobile devices _(in development)_                                      | [App Store](#) | [Google Play](#) | —                                                      |

> Links marked `(#)` are placeholders — the apps are not yet published to those stores.

## Screenshots

### color-surface

![color-surface screenshot](https://github.com/Design-Leaders-Finland/.github/raw/main/profile/screenshots/color-surface.png)

### naoentendonada

![naoentendonada screenshot](https://github.com/Design-Leaders-Finland/.github/raw/main/profile/screenshots/naoentendonada.png)

### wall

![wall screenshot](https://github.com/Design-Leaders-Finland/.github/raw/main/profile/screenshots/wall.png)

### ok-timelapse

![ok-timelapse screenshot](https://github.com/Design-Leaders-Finland/.github/raw/main/profile/screenshots/ok-timelapse.png)

## Our Principles

- **Privacy first** — None of our apps collect analytics, telemetry, or personal data.
- **No ads** — Ever.
- **One-time purchase** — 1 EUR, no subscriptions.
- **Open source** — All code is published under the Apache 2.0 licence.
- **Platform support** — We target current major versions only: Android 13+, iOS 18+, macOS 15+, Windows 11+, and the last two major browser versions for web.

## Tech Stack

All apps are built with:

- **Flutter 3.44.2** / **Dart 3.12.2**
- Consistent CI/CD pipelines (GitHub Actions): format → analyse → test → build matrix
- Releases triggered by `v*` git tags only
- Supply-chain security: CodeQL, Dependabot

## GitHub Actions available via this repository

### Setup Flutter SDK

Uses hardcoded commit hash versions, to comply with the supplychain security setting, to prevent accidental dependency updates in the workflow.

```yaml
env:
  FLUTTER_VERSION: "3.44.2" # single source of truth, reused by all jobs

jobs:
  flutter-tests:
    name: Flutter testing
    runs-on: ubuntu-latest

    steps:
      - name: Setup Flutter SDK # local composite action: avoids marketplace actions with unpinned nested steps
        # Install the pinned Flutter SDK used by the repo.
        uses: design-leaders-finland/.github/actions/setup-flutter@1007cbb5267ff846d012044aaccd3c4a39f5969f
        with:
          version: ${{ env.FLUTTER_VERSION }}

      - name: Cache pub dependencies
        # Reuse pub cache to speed up dependency installs.
        uses: actions/cache@55cc8345863c7cc4c66a329aec7e433d2d1c52a9 # v6.1.0
        with:
          path: |
            ~/.pub-cache
            ~/AppData/Local/Pub/Cache
          key: ${{ runner.os }}-pub-${{ env.FLUTTER_VERSION }}-${{ hashFiles('**/pubspec.lock') }}
          restore-keys: |
            ${{ runner.os }}-pub-${{ env.FLUTTER_VERSION }}-
```

## Contributing

Each app has its own repository, issue tracker, and contributing guide. See the individual repos for details.

## License

All repositories are licensed under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) unless stated otherwise.

© Design Leaders Finland
