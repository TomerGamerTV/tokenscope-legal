# TokenScope Privacy Policy

**Effective date:** 2026-11-06
**Last updated:** 2026-11-06

TokenScope is an independent allowance dashboard for ChatGPT/Codex and Claude
subscriptions. It does not sign in to those services, does not read your
messages or transcripts, and never receives your provider password, OAuth
token, session cookie or API key.

> Operator and contact details are below. The optional Sites relay is operated
> by the project on OpenAI Sites; direct/LAN, Tailscale, Cloudflare, localhost.run
> and ntfy modes do not involve a project-hosted service.

## 1. Who is responsible

The data controller for the TokenScope app and the TokenScope companion is
TomerGamerTV ("we", "us"). Contact: tomergamertv+tokenscope@gmail.com.

The app is distributed through Apple's App Store. Apple processes App Store
purchases, iCloud and push delivery under Apple's own privacy policy. The
companion is distributed separately and runs on a computer that you control.

## 2. Summary

- Usage readings are produced on your own computer by the companion, from the
  official OpenAI Codex client or Claude Code's documented status-line output.
- Readings are encrypted on the computer before they leave it only if you
  choose a hosted connection method. With a direct/LAN connection they stay on
  your network.
- The optional hosted relay stores encrypted envelopes, routing identifiers and
  push registration metadata. It does not hold the content key and cannot read
  allowance percentages.
- No analytics, advertising, tracking, fingerprinting or sale of personal data.
- Everything the app stores on your device can be removed by removing the
  account/connection; hosted channels can be revoked from the companion.

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
| Sites relay | Encrypted envelopes uploaded to our relay | Our hosting provider and us (metadata only) |

Tunnel and ntfy providers are third parties with their own terms and retention.
Choose a method that matches your threat model. Route secrecy is not
authentication; envelope encryption and publisher verification are.

## 5. Hosted relay: what we store and why

If you use the Sites connection method (`--mode sites`), the companion uploads
the encrypted envelope to the TokenScope relay hosted on OpenAI Sites
(hosting region controlled by that provider). The relay stores:

- a random channel identifier derived from the publisher's public identity;
- the latest encrypted envelope and a monotonic sequence number;
- the envelope size, timestamps and last-update time;
- if you enable update hints, a device push token, its environment
  (sandbox/production), the chosen hint style and per-device send timestamps;
- standard request metadata that any internet service receives (IP address,
  user agent, time). Our hosting provider may keep short-lived operational logs.

The relay does not receive the content key, the private signing key, provider
credentials, prompts, responses, email addresses or names. We cannot decrypt
your allowance readings. The relay serves only the latest packet; it is not a
history service.

Retention: the latest envelope is kept while the channel is active. Channels
with no activity for 30 days are deleted, together with their device
registrations. Revoking a connection from the companion deletes the hosted
channel and its devices. Deleting the app removes local keys and caches; it does
not by itself delete a hosted channel that another device still uses.

## 6. Push notifications

Update hints are optional and off unless you enable them. If enabled, Apple
Push Notification service delivers them through our relay. Visible hints contain
only a generic title and the text "New encrypted usage reading"; allowance
numbers are decrypted on your device by the notification service extension. The
relay stores the push token until you disable hints, revoke the connection or the
channel expires.

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
steps at your request (providing the app and relay); legitimate interests
(keeping the service secure and operational, preventing abuse); consent (optional
push hints, optional iCloud sync, optional support purchases); and legal
obligations (tax and accounting for purchases). You can withdraw consent at any
time by turning the feature off.

## 11. Your choices and rights

- **Access / portability:** the app shows the readings it holds; the companion
  exposes the current summary locally.
- **Delete local data:** remove an account or connection in Settings, or delete
  the app.
- **Delete hosted data:** run `tokenscope-companion revoke --endpoint <relay>`
  on the computer, or remove the connection and let the channel expire.
- **Disable hints / iCloud:** turn the switch off in TokenScope settings.
- **Refunds:** contact Apple; we cannot process App Store refunds.
- **EEA/UK rights:** access, rectification, erasure, restriction, objection and
  complaint to a supervisory authority. Contact `tomergamertv+tokenscope@gmail.com`.
- **California rights:** know, delete, correct and opt out of sale/sharing. We
  do not sell or share personal information as those terms are defined.

We may need to verify that a request relates to you; because we hold almost no
identifying data, we may ask for the channel identifier from the companion.

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

Our relay is hosted by OpenAI Sites; Apple, tunnel and ntfy providers may
process data in other countries. Where required, transfers rely on standard
contractual clauses or the provider's equivalent safeguards. Because readings
are end-to-end encrypted, transferred content remains unreadable to us.

## 15. Third-party services

- Apple: App Store, StoreKit, iCloud, APNs — https://www.apple.com/legal/privacy/
- OpenAI Sites: relay hosting — https://openai.com/policies/privacy-policy/
- Optional: Cloudflare, localhost.run, Tailscale, ntfy.sh, each under its own
  policy and only when you select that method.
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
