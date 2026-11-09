# Release notes

## 1.0 — SubFuse

- The full SubFuse release succeeds SubFuse Beta, using the existing updater and preserving profiles, remembered sign-ins, costs, renewals, refresh preferences and widget identity.
- Add daily usage history, compact subscription graphs, an expandable Home graph and Combined Usage with comparable credits. Include supported ChatGPT Pro 100 mapping.
- Review weekly allowance efficiency and eligible unused-value estimates, with gaps and unsupported data kept explicit.
- Refine the dark interface, provider accents, renewal colours and desktop widgets; keep details in each subscription's three-dot settings.
- Retain periodic background refresh and add a separate daily history task with pause/removal controls.
- Carry history in encrypted portable profile files. Private preview data remains separate and can be explicitly exported/restored.
- Includes the audited history, scheduling, storage validation and session-lifetime fixes from the completed private version.

Existing Beta 0.9+ users can choose **Check for Updates…**. History starts with fresh readings; past activity cannot be reconstructed. Requires Apple Silicon and macOS 14+. The app is ad hoc signed, not Apple Developer ID signed or notarized.

## 0.15 — portable session archives

- Copy one local profile to a password-protected `.subfuse` file, then restore it beside existing profiles on another Mac.
- Include all saved subscriptions, usage, costs and renewals, plus the profile’s remembered Claude/Cursor website stores. ChatGPT and Gemini still use the destination Mac’s signed-in desktop apps.
- Reject wrong passwords, changed files, unsafe paths and existing sign-in collisions before restoring data. Recover interrupted restores before website-store cleanup.
- Require SubFuse to be idle. If a selected website store was used this launch, quit/reopen before exporting; turn off scheduled refresh first.
- No SubFuse account, upload, saved password or sync. Anyone with the file and password can use its sessions, and providers can expire them.
- Validated with synthetic store round trips and an isolated WebKit marker on macOS 27.2; live provider sessions have not been transferred between two Macs in release testing.

## 0.14.1 — Antigravity background startup

- Update usage and Refresh all now open Antigravity in the background if needed, wait for its local account service, and refresh usage.
- An already-running app is reused. Antigravity remains running afterward; scheduled refreshes still require it to be running.
- Startup has a time limit. Sign-in, account mismatch, and other failures preserve the last saved reading.
- Verified live with Antigravity 2.29.0 and a Starter Quota account, starting from a fully closed app.

## 0.14 — Dark desktop widgets

- All three sizes now share the SubFuse dashboard’s purple Fuse mark, charcoal surfaces, and provider icons.
- Violet bars show remaining allowance. Expired and unavailable readings use a muted, dashed track.
- The small widget highlights a single current reading. Medium and large widgets keep subscriptions in attention order.

## 0.13.1 — Saved usage widget fix

- Fixed a startup crash that could prevent the widget from loading in any size.
- The widget now reads the existing SubFuse profile file when shared storage is unavailable or profile migration fails. A signed-out profile still shows an empty widget.
- The fallback is automatic and grants read-only access to the single saved file in Application Support.

## 0.13 — Saved usage widget

- Add a small, medium, or large macOS widget to see saved allowances for the active profile. Subscriptions needing attention appear first.
- Open a subscription’s detail sheet directly from the widget. Freshness dots and reset labels age from saved timestamps while the app is closed.
- Use a shared container when macOS grants access. The app retains Application Support as its fallback and preserves the original profile file after migration.

## 0.12.1 — Antigravity connection repair

- Fixed Gemini connection failures with Antigravity's standalone desktop runtime by trying authenticated HTTP after HTTPS on verified process-owned local listeners.
- Preserved loopback-only requests, in-memory tokens, extension-token selection, account checks, and saved readings after failure.
- Verified live with Antigravity 2.28.2 and a Starter Quota account: both allowance pools matched, refresh succeeded, and the subscription persisted across restart. Other plans and versions remain unverified.
- Passed 89 Gemini, 59 refresh, and 146 background-refresh checks, plus the full core Swift and production JavaScript suites and signed release verification.

## 0.12 — Gemini through Antigravity

- Added Gemini through the running Antigravity desktop account service, bringing support to four providers: Claude, ChatGPT, Cursor, and Gemini.
- Displays reported allowance pools, remaining usage, explicit reset times, and unavailable or outdated readings without inventing quota.
- Supports individual, bulk, and optional background refresh, with account checks and preserved readings after failure.
- Includes the existing subscription names, manual costs/currencies, renewals, trials, calendar reminders, local profiles, and freshness confirmation.
- Keeps the Antigravity runtime token in memory; no Google sign-in or credentials are imported into SubFuse.
- Passed automated and synthetic UI verification. Live Antigravity account verification is pending; older readings may be cached and the internal interface may change.

Requires Apple Silicon and macOS 14 or newer. This beta is ad hoc signed, not Apple-notarized.

## 0.11 — Background usage refresh

- Added optional automatic usage refresh in Settings, with 5-, 15-, 30-, and 60-minute choices saved per local profile. It starts off, with 15 minutes selected.
- Refreshes the active profile while SubFuse is running, including when another app has focus. Sleep and quitting pause refresh; overdue intervals produce one catch-up attempt.
- Added passive status, attempt counts, and the last fully successful refresh time. Automatic attempts never open sign-in windows.
- Kept saved readings and timestamps intact after provider or save failures, with bounded retry backoff.
- Prevented overlap with manual refresh and connection windows, and rejected late results after cancellation or profile changes.
- Preserved existing profiles, remembered sign-ins, costs, renewals, and signed app updates.

## 0.10.1 — Cursor refresh repair

- Fixed a false sign-in prompt that prevented Cursor subscriptions from refreshing after the account dashboard changed.
- Preserved existing remembered accounts, subscription details, costs, and renewals.
- Kept account verification before and after usage collection, with compatibility for older dashboard routes.

Includes the one-click refresh changes merged for 0.10:

- Claude and Cursor updates reuse remembered sign-ins in the background. Individual updates show the connection window only when needed.
- Added **Refresh all** inside the top-right status pill for every subscription in the current profile.
- Bulk refresh saves successful readings and skips accounts needing help, with a short partial-failure message.
- Automatic attempts time out safely; failed updates preserve previous readings and duplicate refreshes are blocked.
- Existing profiles, sign-ins, costs, and renewal schedules stay compatible.

## 0.9 — SubFuse Beta

- Added built-in update checks in the app menu and Settings.
- Added automatic update checking, which can be switched off.
- Added verification of signed update feeds and app downloads.
- Renamed the app SubFuse Beta.
- Preserved existing local profile storage and provider connections.

Supports Claude, ChatGPT, and Cursor only. Requires Apple Silicon and macOS 14 or newer. This beta is not Apple-notarized.

## Earlier local versions

Version 0.8 added Cursor account dashboards and remembered Cursor sign-ins, building on Claude, ChatGPT Work/Codex usage, local profiles, manual costs, and renewal tracking.
