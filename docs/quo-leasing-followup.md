# LEASING Inbox Hourly Follow-Up Agent

Automated follow-up on the Quo LEASING line. Runs hourly, finds people who
reached out and never got taken care of, and asks whether they were helped —
capturing name and email while it's there.

## Configuration

| Setting | Value |
|---|---|
| Inbox | LEASING — +19092779818 (`PNt6u9ghjz`) |
| Schedule | Hourly, 7am–7pm Pacific, every day |
| Cron (UTC) | `0 14-23,0-2 * * *` |
| Mode | **DRAFT ONLY** — reports proposed texts, sends nothing |
| Lookback | 24 hours per run |

## Who qualifies

A contact is texted only if ALL of these hold:

1. Inbound text or missed call within the lookback window
2. No human reply from staff, OR helped but name/email still missing
3. No follow-up already present in the thread (full thread is read first)
4. Not one of our own numbers or staff cells
5. Not a solicitation
6. We don't already have both name and email
7. They have not asked to stop

## Exclusion list — our own numbers

Never text these. The LEASING line sends internal lead handoffs to staff, so
they appear as ordinary conversations.

    +19092779818  LEASING (self)
    +19092881991  Rob Galvan Main Chat
    +19093219121  Chris Formica Main Line
    +16266244171  Maintenance Line
    +18003256835  800 NUMBER
    +16266999776  Executive Line
    +19096555955  Chris Martinez Main Line
    +16264881905  Rob Galvan (cell)

## Solicitation filter

Skipped, not texted: realtors requesting showings, escrow/title/mortgage
pitches, wholesalers and cash buyers, lead-gen and referral-fee offers,
marketing spam. When ambiguous, skip and flag for human review.

## Auto-replies that do NOT count as a human reply

    "Hey! Thanks for your message, we'll get back to you shortly."
    "Hi! Thank you for contacting Bright Path Property Management. This is a
     text line for rental inquiries..."

## Message template

> Hi! This is Bright Path Property Management following up on your rental
> inquiry — did we get you what you needed? If not, I'm happy to help. Could I
> also get your name and best email so we can send you matching listings?

Adapts per recipient: uses a known name, references the property when known,
and is written in Spanish when the thread is in Spanish.

## Going live

Draft mode reports what it would send without sending. After reviewing a week
of drafts, switching to live send requires updating the Routine prompt and
pre-approving the `send-message` tool.

## Notes

- Cron is fixed UTC and does not follow daylight saving. After 1 Nov 2026 this
  window becomes 6am–6pm Pacific until it is adjusted.
- Routines share no memory between runs. Deduplication works by reading the
  Quo thread itself, which is durable and survives restarts.
