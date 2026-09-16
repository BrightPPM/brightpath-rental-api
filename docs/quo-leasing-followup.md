# LEASING Inbox Follow-Up and Lead Handoff

Two stages on the Quo LEASING line.

**Stage 1, follow up.** Find people who reached out and never got taken care
of, and ask whether they were helped.

**Stage 2, hand off.** Once a thread is qualified, connect the lead to their
assigned agent and tell the agent about the lead.

## Configuration

| Setting | Value |
|---|---|
| Inbox | LEASING, +19092779818 (`PNt6u9ghjz`) |
| Schedule | Hourly, 7am to 7pm Pacific, every day |
| Cron (UTC) | `0 14-23,0-2 * * *` |
| Mode | **DRAFT ONLY.** Reports proposed texts, sends nothing |
| Lookback | 24 hours per run |

## Stage 1: follow up

A contact gets a follow-up only if ALL of these hold:

1. Inbound text or missed call within the lookback window
2. No human reply from staff, OR helped but name or email still missing
3. No follow-up already present in the thread (full thread is read first)
4. Not one of our own numbers or staff cells
5. Not a solicitation
6. We do not already have both name and email
7. They have not asked to stop
8. Fewer than three consecutive unanswered outbound messages

### Follow-up template

> Hi! This is Bright Path Property Management following up on your rental
> inquiry. Did we get you what you needed? If not, I'm happy to help. Could I
> also get your name and best email so we can send you matching listings?

Adapts per recipient: uses a known name, references the property when known,
and is written in Spanish when the thread is in Spanish.

No STOP or opt-out language is appended. No em dashes.

## Stage 2: qualified lead handoff

### What makes a thread qualified

All three must be known:

1. **Name**
2. **Phone number**
3. **Property they are interested in**

Email is useful but not required to qualify.

The property must then be looked up in the Listing Tracker (see
`docs/data-sources.md`). Proceed only if:

- The property is in the tracker
- Its Status is **Active**
- An agent resolves from the Agent column

Agent resolution: a blank Agent field or "Bright Path Direct" means **Chris
Martinez**. A showing agent named in the Notes column is NOT the listing agent.
Use the agent's phone and email from the tracker roster sheet.

### Do not hand off, flag instead

- Property is not in the tracker. Never invent an agent or a listing link.
- Status is Pending or Placed. The lead needs different information.
- Agent cannot be resolved.
- A handoff already exists in the thread. Never hand off the same lead twice.

### Two messages, in this order

**1. To the lead**, from the LEASING line:

> Great news [Name]! For [address], your leasing agent is [Agent]. You can
> reach them directly at [agent phone]. Give them a call, and if they don't
> answer a text is perfectly fine. They will be reaching out soon as well.
> Thank you for contacting Bright Path Property Management!

**2. To the assigned agent**, from the LEASING line:

> Hi [Agent], qualified LEASING lead for [address] ([rent]). Name: [Name].
> Phone: [lead phone]. [Email if known.] They are interested in [property].
> Came in on LEASING (909) 277-9818. [Language or other constraints.] I gave
> them your number and told them to call, or text if you don't pick up. Please
> reach out.

Send to the agent phone listed on the tracker roster sheet. Include the showing
agent from the Notes column if one is named.

### Handoff is an exception to the do-not-text list

The do-not-text list below blocks **follow-up** texts to Bright Path numbers,
so the agent never receives a "were you helped" message. It does NOT block a
deliberate Stage 2 handoff. Texting an assigned agent about a lead is the
intended behavior.

The owner's test cell, +16266780656, is blocked for everything including
handoffs.

## Exclusion list, our own numbers

Never send a follow-up to these. The LEASING line sends internal lead handoffs
to staff, so they appear as ordinary conversations.

    +19092779818  LEASING (self)
    +19092881991  Rob Galvan Main Chat
    +19093219121  Chris Formica Main Line
    +16266244171  Maintenance Line
    +18003256835  800 NUMBER
    +16266999776  Executive Line
    +19096555955  Chris Martinez Main Line
    +16264881905  Rob Galvan cell
    +16266780656  Owner personal cell, test number. Blocked for everything.

## Solicitation filter

Skipped, never texted: realtors requesting showings, escrow, title and mortgage
pitches, wholesalers and cash buyers, lead-gen and referral-fee offers,
marketing spam. When ambiguous, skip and flag for human review.

## Auto-replies that do NOT count as a human reply

    "Hey! Thanks for your message, we'll get back to you shortly."
    "Hi! Thank you for contacting Bright Path Property Management. This is a
     text line for rental inquiries..."

## Going live

Draft mode reports what it would send without sending. Switching to live send
requires updating the Routine prompt and pre-approving the `send-message` tool.

Stage 2 may reasonably go live before Stage 1, since the agent notification is
internal and the lead message only repeats information the team would send by
hand anyway.

## Notes

- Cron is fixed UTC and does not follow daylight saving. After 1 Nov 2026 this
  window becomes 6am to 6pm Pacific until it is adjusted.
- Routines share no memory between runs. Deduplication works by reading the Quo
  thread itself, which is durable and survives restarts.
