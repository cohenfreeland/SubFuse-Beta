# Privacy notes

SubFuse Beta stores profiles, subscription labels, account display labels, hashed account identifiers, usage snapshots, manually entered costs, renewal schedules, and per-profile background refresh preferences and attempt summaries in a local `state.json` file. Passwords and authentication tokens are not stored in that JSON file.

When macOS grants shared storage access, SubFuse keeps the live file at `SubFuse/state.json` inside the `group.app.subfuse.local` container. The app verifies the migrated copy and retains `~/Library/Application Support/SubFuse/state.json` as a backup. Application Support remains the live location if the container is unavailable or migration fails.

The sandboxed desktop widget reads the active profile’s saved subscription names, provider and plan labels, usage readings, and timestamps. Its display omits account labels, email addresses, account keys, and sign-in identifiers. The widget has no network entitlement and makes no provider requests.

Claude and Cursor sign-ins use persistent WebKit website data stored separately on this Mac. SubFuse isolates sessions by local profile and account. It does not import credentials from Cursor, Claude Desktop, another browser, or the Keychain. ChatGPT collection asks the installed account service for its signed-in identity and allowance readings.

Gemini collection discovers the same-user Antigravity desktop service and sends account and quota requests only to loopback addresses on this Mac. Its runtime CSRF token stays in memory and is never stored in profile JSON or logged. SubFuse does not import Google OAuth credentials, browser cookies, or Keychain data. Antigravity manages its own Google authentication and may contact its provider to refresh quotas. Account matching uses a provider-specific hash of the normalized email reported by the service; the account display label is stored locally. An email change requires a new subscription, and reassigned organizational emails cannot be distinguished. Removing a Gemini subscription or deleting a local profile does not sign out of Antigravity.

Connecting or refreshing sends account and usage requests to the relevant provider using its normal authentication. Those providers apply their own privacy policies. SubFuse does not read conversations or start AI tasks to measure usage.

Background usage refresh is off by default. When enabled for a local profile, SubFuse periodically makes the same provider requests while the app is running, including when it is not focused. You choose 5, 15, 30, or 60 minutes; timing can be delayed by sleep, ongoing operations, or retry backoff. Only the active profile is refreshed. Disabling the setting, signing out, or quitting stops automatic refresh. No new analytics or SubFuse server is involved.

Checking for updates contacts GitHub to retrieve the appcast; downloading an update contacts GitHub's release hosting. Those services can receive standard network information such as your IP address and request headers. No saved profile, subscription, or billing data is included in the update feed request. Sparkle system profiling is disabled.

There is no SubFuse cloud account, cross-device sync, or built-in analytics service. Local profiles are organizational tools, not separate password-protected accounts.

Use **Forget sign-in** to remove a Claude or Cursor website session while retaining the saved subscription. Removing the account's last subscription or deleting its profile also cleans up its website session. Signing out of a local profile retains it for later use. Removing a SubFuse subscription does not cancel the provider's plan.

GitHub issues are public. Do not post authentication data or personal account information there.
