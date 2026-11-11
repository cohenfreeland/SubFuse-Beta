# Privacy notes

SubFuse stores profiles, subscription labels, account display labels, hashed account identifiers, usage snapshots, timestamped history observations, plan mappings, price-change markers, collection preferences, manually entered costs, renewal schedules, and per-profile background refresh preferences and attempt summaries in a local `state.json` file. Passwords and authentication tokens are not stored in that JSON file.

When macOS grants shared storage access, SubFuse keeps the live file at `SubFuse/state.json` inside the `group.app.subfuse.local` container. The app verifies the migrated copy and retains `~/Library/Application Support/SubFuse/state.json` as a backup. Application Support remains the live location if the container is unavailable or migration fails.

When the shared profile file is unavailable, the widget can read the existing `~/Library/Application Support/SubFuse/state.json` file. Its additional permission is read-only and covers that single file.

The sandboxed desktop widget reads the active profile’s saved subscription names, provider and plan labels, usage readings, and timestamps. Its display omits account labels, email addresses, account keys, and sign-in identifiers. The provider icons and allowance bars are drawn locally from the same saved readings. The widget has no network entitlement and makes no provider requests.

Claude and Cursor sign-ins use persistent WebKit website data stored separately on this Mac. SubFuse isolates sessions by local profile and account. It does not import credentials from Cursor, Claude Desktop, another browser, or the Keychain. ChatGPT collection asks the installed account service for its signed-in identity and allowance readings.

Manual Update usage and Refresh all may open the installed Antigravity desktop app in the background when needed and leave it running afterward. Scheduled refresh does not launch Antigravity. SubFuse does not switch its Google account or bypass sign-in.

Gemini collection discovers the same-user Antigravity desktop service and sends account and quota requests only to loopback addresses on this Mac. Its runtime CSRF token stays in memory and is never stored in profile JSON or logged. SubFuse does not import Google OAuth credentials, browser cookies, or Keychain data. Antigravity manages its own Google authentication and may contact its provider to refresh quotas. Account matching uses a provider-specific hash of the normalized email reported by the service; the account display label is stored locally. An email change requires a new subscription, and reassigned organizational emails cannot be distinguished. Removing a Gemini subscription or deleting a local profile does not sign out of Antigravity.

Connecting or refreshing sends account and usage requests to the relevant provider using its normal authentication. Those providers apply their own privacy policies. SubFuse does not read conversations or start AI tasks to measure usage.

Background usage refresh is off by default. When enabled for a local profile, SubFuse periodically makes the same provider requests while the app is running, including when it is not focused. You choose 5, 15, 30, or 60 minutes; timing can be delayed by sleep or ongoing operations. From version 1.0.1, retry backoff applies when no subscriptions can refresh; partial failures keep the selected frequency. Only the active profile is refreshed. Disabling the setting, signing out, or quitting stops automatic refresh. No new analytics or SubFuse server is involved.

Checking for updates contacts GitHub to retrieve the appcast; downloading an update contacts GitHub's release hosting. Those services can receive standard network information such as your IP address and request headers. No saved profile, subscription, or billing data is included in the update feed request. Sparkle system profiling is disabled.

There is no SubFuse cloud account, cross-device sync, or built-in analytics service. Local profiles are organizational tools, not separate password-protected accounts.

Use **Forget sign-in** to remove a Claude or Cursor website session while retaining the saved subscription. Removing the account's last subscription or deleting its profile also cleans up its website session. Signing out of a local profile retains it for later use. Removing a SubFuse subscription does not cancel the provider's plan.

GitHub issues are public. Do not post authentication data or personal account information there.


## Daily history

Daily history stores local observations and calculation inputs alongside the profile. SubFuse registers a macOS LaunchAgent for 9 AM local time; it may quietly launch the app when closed, including an initial setup attempt. Only the active profile is collected, using existing provider sessions. The Mac must be logged in; sleep can delay collection, and the task does not wake it. No conversations are read and no missing history is invented.

Daily collection is separate from opt-in periodic background refresh. Pause it in **Settings → Daily usage history**, or remove its daily task. Reopening the app registers the task again, but a saved pause remains effective. Manual refresh remains available. History and its derived efficiency estimates remain local.

SubFuse 1.0 uses Beta's existing app identity, storage locations and website-store identifiers. Private previews remain separate unless you explicitly export and restore a profile.

## Portable profile files

When you choose **Copy to another Mac…**, SubFuse reads only the chosen profile and its referenced Claude/Cursor website-store directories. The resulting `.subfuse` file contains the profile’s subscriptions, saved readings, usage history, billing details and those website sessions. ChatGPT and Gemini desktop credentials are not included. SubFuse never uploads the file; you choose its destination and copy it yourself. There is no account or sync service.

The archive uses AES-GCM authenticated encryption with a password-derived key, a random salt and PBKDF2-HMAC-SHA256 at 200,000 iterations. The archive is created with owner-only permissions. The password is used for the operation, then cleared from the form; it is not stored in profile JSON, Keychain, logs or the filename. There is no password recovery. Anyone with the file and password can use included sessions until the provider expires or revokes them.

Restore decrypts and validates before writing, refuses an existing website-store ID, and adds the imported profile beside existing profiles. Temporary restore staging contains decrypted website data in owner-only local directories. A recovery journal lets SubFuse complete or roll back an interrupted restore before ordinary store cleanup; staging is removed after completion. The file you selected remains where you put it. Delete copies you no longer need.
