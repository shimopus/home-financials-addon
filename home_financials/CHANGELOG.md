# Changelog

All notable changes to Home Financials are documented here.

## v1.3.0 - 2026-11-28

### Added
- **Browser Companion API & pairing**: Opt-in `8100/tcp` Companion API port in add-on network configuration, token pairing and last-sync summary under **Settings → Browser Companion**, and `Companion` / `Manual` badges in **Last uploads** on Account screens.
- **Vanguard broker support**: Add Vanguard accounts with a configurable **Settlement fund** (default `VMFXX`) and upload multi-section Vanguard `OfxDownload.csv` exports (automatically skipping 401(k) sections), plus open-lot sync support for non-Reserve Taxable accounts.
- **Confirm sold for omitted holdings**: Positions absent from a newer snapshot remain marked **Stale** until confirmed sold on the Account screen or opted into during upload preview.

### Changed
- **Snapshot precedence**: Uploading a Positions or Lot file with a file date on or before the stored snapshot now requires explicit override confirmation in Preview.
- **Reserve-pool Taxable accounts**: Lot files are optional for Reserve-pool Taxable accounts, Reserve-pool notices explain that they are excluded from harvesting, and reinvestment warnings are suppressed for Reserve-pool accounts and securities matching a Reserve holding's Identical group.
- **Holding deep-links**: Linking to an Account screen with a symbol filter scrolls to and highlights the matching holding row.

## v1.2.0 - 2026-11-27

### Added
- Morning price updates in your Home Assistant household timezone (09:00 local) plus intraday quotes at 12:30 and 15:30 ET on open NYSE market days, with screens and alerts distinguishing closing prices from intraday timestamps.
- Timestamped application logging to standard output for startup configuration, scheduled and catch-up job runs, price fetches, confirmed uploads, and Telegram alert decisions (with API keys and tokens redacted).
- Versioned release notes published to GitHub Releases and the Home Assistant add-on Changelog tab.

### Changed
- Redesigned the Strategy screen with URL-backed `Classes`, `Targets`, `Funds`, and `Groups` tabs, a strategy readiness summary, deep-links from Today, Holdings, Plan, and Setup, fund search and reserve/unheld filters, and inline fund editing.
- Consolidated Today, Holdings, Taxes, Plan, and top-bar reads into single screen-shaped requests for faster loading.

### Fixed
- Decided missing realized sales by Proceeds (falling back to shares when history lacks proceeds), eliminating false warnings caused by 2-decimal share rounding in Schwab Realized files.
- Aligned Wash sale blocking with Closed Lot basis adjustments and Proceeds coverage so covered gain sales no longer falsely block replacement buys while basis-adjusted losses and partial coverages still block.
- Counted Reserve-pool holdings without a Composition in a **Held in a Reserve pool** Drift row without triggering missing-composition warnings, matching the Asset classes total to headline Invested.
- Marked only closing prices older than the latest closes as Stale so Positions-file fallback prices (such as T-bills) are shown as dated instead.
- Fixed dark-mode contrast for subtle and light ink buttons and reorder controls.
