# Privacy notes

SubFuse Beta stores profiles, subscription labels, account display labels, hashed account identifiers, usage snapshots, manually entered costs, and renewal schedules locally at `~/Library/Application Support/SubFuse/state.json`. Passwords and authentication tokens are not stored in that JSON file.

Claude and Cursor sign-ins use persistent WebKit website data stored separately on this Mac. SubFuse isolates sessions by local profile and account. It does not import credentials from Cursor, Claude Desktop, another browser, or the Keychain. ChatGPT collection asks the installed account service for its signed-in identity and allowance readings.

Connecting or refreshing sends account and usage requests to the relevant provider using its normal authentication. Those providers apply their own privacy policies. SubFuse does not read conversations or start AI tasks to measure usage.

Checking for updates contacts GitHub to retrieve the appcast; downloading an update contacts GitHub's release hosting. Those services can receive standard network information such as your IP address and request headers. No saved profile, subscription, or billing data is included in the update feed request. Sparkle system profiling is disabled.

There is no SubFuse cloud account, cross-device sync, or built-in analytics service. Local profiles are organizational tools, not separate password-protected accounts.

Use **Forget sign-in** to remove a provider session while retaining the saved subscription. Removing the account's last subscription or deleting its profile also cleans up its website session. Signing out of a local profile retains it for later use. Removing a SubFuse subscription does not cancel the provider's plan.

GitHub issues are public. Do not post authentication data or personal account information there.
