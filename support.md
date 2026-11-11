# TokenScope Support

TokenScope shows ChatGPT/Codex and Claude subscription allowances. It does not
sign you in to those services and cannot fetch allowances by itself; a small
companion program on your own computer provides the readings.

Contact: `tomergamertv+tokenscope@gmail.com`. Never send pairing codes, QR images, private keys,
tokens or provider credentials.

## Before you start

- iPhone/iPad on iOS/iPadOS 26 or later (Watch features need watchOS 26+).
- A Mac (Node 22+), Windows PC (Node 22+) or Linux computer that stays on.
- The official Codex client signed into your ChatGPT account, or Claude Code
  signed into your Claude account.
- The official `tokenscope-companion` package from npm or a TokenScope release.
  Do not install a similarly named package from another publisher.

## Set up Codex readings

1. Install Node 22 or later. Then either run
   `npx tokenscope-companion@0.2.7 login` or install it once with
   `npm install -g tokenscope-companion@0.2.7` (preferred for a persistent
   publisher and for `setup-claude`).
2. Complete the official ChatGPT sign-in in your browser.
3. Start a publisher. The managed route needs no setup:
   `tokenscope-companion start --mode opentunnel`
   (or `--mode sites --endpoint https://YOUR_RELAY` for a relay you deploy;
   alternatives: `--mode ntfy`, `--mode direct`, `--mode cloudflare`,
   `--mode localhost`, `--mode tailscale --endpoint https://…`, or
   `--mode external --endpoint https://YOUR_TUNNEL`). TokenScope does not
   provide a relay; OpenTunnel is a third-party tunnel service.
4. In TokenScope, open **Settings → Connections** and scan the private
   `pairing.svg` the companion saved (or paste `pairing-url.txt`).
5. Confirm the computer name and publisher fingerprint, then wait for the first
   reading. Keep the companion running.

`--label "My Mac"` names the account on your devices. Without a label the
subscription plan is shown.

## Set up Claude readings

1. Update Claude Code and sign in normally.
2. Run `tokenscope-companion setup-claude` from a global install. It backs up
   Claude settings, adds a status line and leaves unrelated settings alone. If a custom status line
   already exists, it refuses to overwrite it; use the bundled
   `CLAUDE_SETUP_PROMPT.md` for a script-aware integration.
3. Send one normal message in Claude Code. The status line writes a normalized
   reading; no transcript is saved.
4. Start the separate Claude publisher:
   `tokenscope-companion start --provider claude --mode opentunnel`
   (or `--mode sites --endpoint https://YOUR_RELAY` for your own relay)
5. Pair its QR in TokenScope. Codex and Claude can run side by side.

Claude readings update only when Claude Code itself supplies allowance fields.
Opening the app or refreshing cannot force an idle Claude session to fetch
quotas.

## "Refresh needed", stale or unknown readings

- A timestamp and "cached reading" label mean the number is real but old. The
  app will not relabel old data as fresh.
- "Refresh required" after a reset time means the allowance window has passed
  and no newer observation has arrived.
- Unknown (`—`) means the provider did not supply that field. It is not zero.
- Common causes: the computer is off or asleep, the companion is stopped, the
  provider session is signed out, the phone has no network, or iOS background
  refresh is delayed. iOS decides when background refresh runs.
- Fix: start the companion, confirm it prints an encrypted snapshot, then pull
  to refresh in TokenScope.

## Run the companion in the background

- Install it once, then register a background publisher:
  `npm install -g tokenscope-companion@0.2.7`, then
  `tokenscope-companion service install --provider claude --mode opentunnel`.
- `tokenscope-companion service status` reports whether it is running;
  `tokenscope-companion service uninstall` stops and removes it.
- On macOS it is a launchd agent, on Linux a systemd user unit, and on Windows a
  per-user Scheduled Task that starts hidden. All three start **after you sign
  in**; none is an elevated system service or runs before sign-in.
- Only one background publisher is supported. Stop a manual `start` before
  installing, because both use the same `publisher.lock`.
- `service install` requires a global install; it refuses to run from the
  disposable `npx` cache. Add `--interval 1800` to publish every 30 minutes.
- Logs are written to `service.log` in the private directory (`0600` on macOS/Linux). They contain status lines and paths, never keys or the pairing URL.
- Reinstall the service after upgrading or changing Node, because the agent
  records an absolute Node path.

## Companion says "Publisher lock"

- The lock stops two publishers from writing to the same private directory. The
  message names the lock path and the owning process ID.
- Stop the other publisher, or confirm and end that process. On Windows,
  `Get-Process -Id <pid>` in PowerShell shows whether it is still running.
- Companion 0.2.6 and later remove a lock automatically when its owner has
  exited, including an empty lock left by a crash. On an older version, update
  first (`npx tokenscope-companion@0.2.7 …`); delete `publisher.lock` manually
  only after confirming the reported process is gone.
- Default directories: `~/.tokenscope` for Codex and `~/.tokenscope-claude` for
  Claude (`%USERPROFILE%\.tokenscope` and `%USERPROFILE%\.tokenscope-claude` on
  Windows).
- Never delete a lock while its publisher is running; both processes could
  corrupt the private pairing state.

## Connections and privacy

- Pairing keys stay on your devices. Envelopes are encrypted; even a relay you
  host or the managed OpenTunnel route cannot read percentages.
- OpenTunnel is operated by a third party. It sees connection metadata (IP
  addresses, timing, route name) but not usage values; stop the companion and
  remove its tunnel state if you do not want that mode.
- Remove a connection in **Settings → Connections** to delete its local keys and
  cache on that device.
- On the computer, `tokenscope-companion revoke --endpoint <relay>` deletes the
  channel and its device registrations from that relay.
- Stopping and deleting the companion's private directory rotates its keys.
  Do this only when you intend to re-pair every device.
- A pairing QR or URL is as sensitive as a password. Never post it in a support
  request, screenshot or issue.

## Tips and purchases

- **Settings → Leave a tip** offers three optional one-time non-consumable
  purchases. Each permanently unlocks the extra color themes, meter styles and
  icons for that Apple Account; all customization is already free during the
  prerelease, so tips are optional support.
- Tips are not charitable donations and not subscriptions.
- Use **Restore purchases** after reinstalling or on another device signed into
  the same Apple Account.
- Refunds and billing are handled by Apple at
  https://reportaproblem.apple.com. TokenScope cannot issue refunds.
- If a tip is pending, the unlock appears after Apple approves it.

## Delete your data

- **Local:** remove accounts/connections in the app, then delete the app.
- **Hosted relay:** revoke from the companion (above), or let the channel expire
  after 30 days of inactivity.
- **iCloud:** turn off iCloud sync in TokenScope, then remove the app's iCloud
  data in Apple Settings if desired.
- **Support email:** ask us to delete correspondence at `tomergamertv+tokenscope@gmail.com`.

## Known limitations

- The computer must stay online to produce fresh readings.
- Claude readings depend on Claude Code's documented status-line output; API-only
  sessions may have no subscription allowance fields.
- Background widget/notification delivery is scheduled by iOS and is best
  effort.
- Windows and Linux companion runtime acceptance is still being validated.
- Watch complications and Live Activities depend on the paired phone.

## Report a problem

Include the app version/build, iOS version, companion version, connection
method, the exact on-screen label ("unknown", "cached", "reset passed") and the
time. Do **not** include emails, account identifiers, QR images, pairing URLs,
tokens or raw provider responses.
