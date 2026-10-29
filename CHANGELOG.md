# Release notes

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
