# iCreate Calendar — architecture

## Why separate from Email

Different release cadence, permissions (calendar vs mailbox), and users who want Calendar without a
full mail stack. Invite deep-links can open Calendar via OS handlers later; they do not require one
binary.

## Scope (v1 research target)

- Local calendars (create / edit / delete events)
- CalDAV accounts
- Day / week / month views with original Slate UI (not Outlook or Google Calendar chrome)
- Later: Google Calendar and Microsoft Graph calendars when OAuth reuse is designed

## Foundation

Prefer **greenfield or a thin CalDAV client** (Rust + SQLite + `icalendar`, or equivalent) over
shipping Lightning inside Email. Evaluate FOSS CalDAV libraries for licence compatibility (MIT /
Apache / MPL OK; avoid AGPL in the default stack).

## Security model

- Credentials in OS keychain only
- Event data local-first on disk
- No iCreate cloud sync unless explicitly enabled later with consent UI
- Provider traffic only to user-configured CalDAV / OAuth endpoints

## Licences

- iCreate-owned code: MIT or Apache-2.0 (dual OK)
- Document third-party notices in `NOTICE` before Alpha
- Catalogue `licence` field updates from `Licence TBA` when chosen

## Phased build

1. Research spike: CalDAV round-trip + local store prototype (no catalogue Install).
2. Original Slate UI shell (day/week/month).
3. Google / Graph OAuth design review (shared patterns with Email where safe).
4. CI installers + update channel.
5. Flip `calendar` in `apps.json` from `research` → `alpha` only after step 4.

## Out of scope for v1

- Embedded mail
- Server-side iCreate hosting of calendars by default
- Cloning Outlook ribbon or Google Material calendar UI
