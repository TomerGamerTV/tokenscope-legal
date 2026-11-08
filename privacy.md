# TokenScope Privacy Policy

**Effective date:** 2026-11-06
**Last updated:** 2026-11-06

TokenScope is an independent allowance dashboard for ChatGPT/Codex and Claude
subscriptions. It does not sign in to those services, does not read your
messages or transcripts, and never receives your provider password, OAuth
token, session cookie or API key.

> Operator and contact details are below. TokenScope does not host readings or a
> relay; Sites mode points at a relay you deploy. Direct/LAN, Tailscale,
> Cloudflare, localhost.run and ntfy are user/third-party hosted.

## 1. Who is responsible

The data controller for the TokenScope app and the TokenScope companion is
TomerGamerTV ("we", "us"). Contact: tomergamertv+tokenscope@gmail.com.

The app is distributed through Apple's App Store. Apple processes App Store
purchases, iCloud and push delivery under Apple's own privacy policy. The
companion is distributed separately and runs on a computer that you control.

## 2. Summary

- Usage readings are produced on your own computer by the companion, from the
  official OpenAI Codex client or Claude Code's documented status-line output.
- Readings are encrypted on the computer before they leave it whenever you use
  a network connection method. With a direct/LAN connection they stay on your
  network.
- TokenScope does not operate a relay or a reading store. If you use Sites mode,
  you deploy and control the relay yourself; your host stores only encrypted
  envelopes and metadata and cannot read allowance percentages.
- No analytics, advertising, tracking, fingerprinting or sale of personal data.
- Everything the app stores on your device can be removed by removing the
  account/connection; your own relay data is removed on that deployment.

## 3. Data handled on your device

The app stores, locally on your iPhone, iPad, Apple Watch and their shared app
group:

- account labels you choose (for example "ChatGPT Plus" or "Claude"), the
  provider, plan label and stable account identifier;
- allowance window titles, used percentages, reset times and the observation
  time supplied by the companion;
- recent usage history derived from those observations;
- appearance, widget, notification and Live Activity preferences;
- optional connection templates if you enable iCloud sync (see section 7).

This local data is not sent to us. If you never enable a hosted connection
method, it never leaves your devices.

Claude Code status-line input is reduced to five-hour and weekly allowance
fields. Context percentage, session cost, prompts, responses, project paths and
token totals are discarded before storage. Raw status-line JSON is not written
to disk.

## 4. Data handled by the companion

The companion runs on your Mac, Windows PC or Linux computer and uses the
official Codex CLI sign-in or Claude Code's own sign-in. Provider credentials,
cookies and transcripts stay with those official clients; the companion does not
read or export them.

The companion exports only current, bounded allowance summaries: provider,
optional account label, allowance window names, percentages, reset/observation
times and a publisher signature. It encrypts each envelope with AES-256-GCM and
signs it with Ed25519. The computer keeps the private signing key and content
key; paired devices receive only the public key, content key and a scoped reader
credential.

Connection methods you can choose:

| Method | What leaves the computer | Who can see metadata |
| --- | --- | --- |
| Direct / LAN | Encrypted envelopes on your local network | Your network operator |
| Tailscale | Encrypted envelopes inside your tailnet | Tailscale, your tailnet |
| Cloudflare Quick Tunnel | Encrypted envelopes through a temporary public URL | Cloudflare |
| localhost.run | Encrypted envelopes through a temporary public URL | localhost.run |
| ntfy | Encrypted envelopes posted to an ntfy topic | ntfy.sh and its network |
| Sites relay (self-hosted) | Encrypted envelopes uploaded to the relay you deploy | You and your hosting provider |
| External tunnel (e.g. OpenTunnel) | Encrypted envelopes through a tunnel you run | Tunnel provider (IP/timing; not HTTP plaintext when TLS terminates locally) |
| OpenTunnel (built in) | Encrypted envelopes through a managed route created by the companion | OpenTunnel (IP/timing, route name and device tunnel identity; not HTTP plaintext) |

Tunnel and ntfy providers are third parties with their own terms and retention.
The built-in OpenTunnel mode creates a tunnel identity and route for you; it does
not create an account or send allowance values, reader credentials or provider
keys to OpenTunnel, because TLS terminates on your computer. You can avoid the
managed route by choosing direct/LAN, Tailscale or a tunnel you run.
Choose a method that matches your threat model. Route secrecy is not
authentication; envelope encryption and publisher verification are.

## 5. Self-hosted Sites relay

TokenScope does not provide or default to a relay. Sites mode (`--mode sites`)
requires `--endpoint https://YOUR_RELAY` pointing at a relay you deploy from
`Services/Relay` in the source, or another compatible server. That deployment is
under your control; the project does not receive its data, keys or logs.

A reference relay stores:

- a random channel identifier derived from the publisher's public identity;
- the latest encrypted envelope and a monotonic sequence number;
- the envelope size, timestamps and last-update time;
- if you enable update hints, a device push token, its environment
  (sandbox/production), the chosen hint style and per-device send timestamps;
- standard request metadata that any internet service receives (IP address,
  user agent, time) in your host's logs.

It does not receive the content key, the private signing key, provider
credentials, prompts, responses, email addresses or names, and cannot decrypt
your allowance readings. It serves only the latest packet; it is not a history
service.

Retention is configured by you. The reference relay deletes channels after 30
days of inactivity, and `revoke --endpoint` deletes a channel and its devices.
Deleting the app removes local keys and caches; it does not delete a channel
another device still uses. Delete that on your own relay.

The project previously ran a test relay for beta builds. Current builds do not
reference it; it is not part of the app and is scheduled for deletion.

## 6. Push notifications

Update hints are optional and off unless you enable them. If you enable them,
your relay sends them through Apple Push Notification service. Visible hints
contain only a generic title and the text "New encrypted usage reading";
allowance numbers are decrypted on your device by the notification service
extension. Your relay stores the push token until you disable hints, revoke the
connection or delete the channel. The project has no APNs credentials for this
feature and cannot send you notifications.

## 7. iCloud (optional)

iCloud sync is off by default. If you enable it:

- appearance preferences use Apple's key-value store;
- connection templates use iCloud Keychain so your other devices can offer the
  same connection;
- purchase proof, widget placement, notification permissions and usage history
  stay device-specific.

Apple processes this data under Apple's terms. We do not operate an iCloud
backend and cannot read your iCloud Keychain items.

## 8. Purchases

Tips and unlocks are processed by Apple through StoreKit. We receive only the
verified transaction result needed to unlock customization (product identifier,
app bundle, environment, revocation state). We do not receive your name,
payment card, billing address or Apple Account email. Apple's privacy policy
governs the purchase.

## 9. What we do not collect

- No analytics SDKs, advertising SDKs, crash-reporting SDKs or tracking pixels.
- No advertising identifier (IDFA) and no App Tracking Transparency prompt,
  because we do not track you across apps or websites.
- No provider passwords, OAuth tokens, cookies, API keys, prompts, transcripts
  or project files.
- No contact list, photos, location, health, microphone or camera access.
- No sale or rental of personal data.

## 10. Legal bases (EEA/UK)

Where the GDPR or UK GDPR applies, we rely on: performance of a contract or
steps at your request (providing the app); legitimate interests (keeping the app
secure and operational); consent (optional push hints, optional iCloud sync,
optional support purchases); and legal obligations (tax and accounting for
purchases). You can withdraw consent at any time by turning the feature off. We
do not operate a service that stores your readings.

## 11. Your choices and rights

- **Access / portability:** the app shows the readings it holds; the companion
  exposes the current summary locally.
- **Delete local data:** remove an account or connection in Settings, or delete
  the app.
- **Delete relay data:** on your own deployment, run
  `tokenscope-companion revoke --endpoint <your relay>`, or remove the channel
  from that service.
- **Disable hints / iCloud:** turn the switch off in TokenScope settings.
- **Refunds:** contact Apple; we cannot process App Store refunds.
- **EEA/UK rights:** access, rectification, erasure, restriction, objection and
  complaint to a supervisory authority. Contact `tomergamertv+tokenscope@gmail.com`.
- **California rights:** know, delete, correct and opt out of sale/sharing. We
  do not sell or share personal information as those terms are defined.

We hold no readings, so a deletion request for relay data must be made on the
deployment you control. We can help identify which settings are local.

## 12. Children

TokenScope is a developer/utility tool and is not directed to children under 13
(or under 16 in the EEA/UK). We do not knowingly collect data from children. If
you believe a child provided data, contact us and we will delete it.

## 13. Security

Transport uses HTTPS/TLS. Envelopes use AES-256-GCM with a random nonce and are
signed with Ed25519; devices enforce per-sender sequence floors to reject
rollback. Credentials are stored in Keychain on Apple devices and in a private
directory with restrictive permissions on the computer. No method is perfectly
secure; protect your devices, keep the companion updated and revoke connections
you no longer use.

## 14. International transfers

We do not transfer readings. Apple, your own relay host, tunnel and ntfy
providers may process data in other countries under their own safeguards and
policies. Because readings are end-to-end encrypted, transferred content remains
unreadable to the relay and its host.

## 15. Third-party services

- Apple: App Store, StoreKit, iCloud, APNs — https://www.apple.com/legal/privacy/
- Your relay host: only if you deploy one; governed by your provider's policy.
- Optional: OpenTunnel, Cloudflare, localhost.run, Tailscale, ntfy.sh, each
  under its own policy and only when you select that method. OpenTunnel is
  operated by a third party, not by the TokenScope project.
- OpenAI Codex and Anthropic Claude Code: your use of those clients is governed
  by their own terms. TokenScope is not affiliated with either company.

## 16. Changes

We may update this policy when the app or service changes. The effective date
and "last updated" date above will change, and material changes will be
described in release notes before they take effect. Continuing to use the app
after an update means you accept the revised policy.

## 17. Contact

TomerGamerTV
`tomergamertv+tokenscope@gmail.com`
Israel

For security reports, please use the same address with "security" in the
subject and do not include pairing codes, QR images or credentials.
