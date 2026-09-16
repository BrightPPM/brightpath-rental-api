# Bright Path Property Management

Property management company. Rental leasing, tenant and owner communication.
Primary tools are Quo for phone and text, Google Drive for records, Buildium
for listings.

## Writing conventions

- **Never use em dashes.** Not in chat replies, not in drafted text messages,
  not in documents. Use periods, commas, or parentheses instead.
- **Do not append STOP or opt-out language** to outbound text messages.

## Before answering anything about properties or agents

Read the Listing Tracker. It is the source of truth for rent, availability, and
agent assignment, and it changes constantly. Link and column meanings are in
`docs/data-sources.md`. Do not answer from memory or from a previous session.

## Reference

| File | Contents |
|---|---|
| `docs/data-sources.md` | Listing Tracker link, Drive folders, how to read them |
| `docs/team-and-inboxes.md` | Agent roster, Quo inbox map, do-not-text list, handoff format, standard replies |
| `docs/quo-leasing-followup.md` | The hourly LEASING follow-up automation spec |

## Hard rules for any Quo automation

1. Never text a Bright Path number or the owner's test cell. The list is in
   `docs/team-and-inboxes.md`.
2. Never send the same follow-up to the same person twice. Re-read the full
   Quo thread before sending anything.
3. Never reply to solicitation.
4. Stop after three unanswered outbound messages to one person.
