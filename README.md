# Invite-only dating prototype

**Working name: "Cove" — not decided, not cleared.** The repo name is a neutral placeholder so nothing has to be undone when the real name lands. See [NAMING.md](NAMING.md) before you print the name anywhere.

A single-file, front-end-only prototype of an invitation-gated dating app built around Apple's ecosystem conventions. No build step, no dependencies, no backend — open `index.html` and it runs.

---

## Run it

```bash
# simplest
open index.html

# or serve it, so clipboard/share APIs behave like production
python3 -m http.server 8000
```

Demo invitation codes (the gate rejects anything else):

```
COVE-2026
MEHR-4417
RAAV-8823
```

State lives in `localStorage` under the key `cove.v1`. **You → Reset this demo** clears it.

## What's in it

| Flow | Detail |
| --- | --- |
| Gate | Invitation code required; invalid codes shake the field; "no code" path opens a waitlist form |
| Sign-in | "Continue with Apple" runs a simulated Face ID sheet |
| Onboarding | Three steps — name/age/city, intent, one profile prompt |
| Discover | One card at a time, 6 seeded people, vouched-by attribution, mutual-circle count, pass / like / vouch |
| Matching | Mutual likes only; a like stays quiet until it's returned |
| Chat | iMessage-shaped thread, typing indicator, auto-replies, sticky glass composer |
| Invites | Exactly 3 single-use codes per member, copy/share, invitation chain, how-the-door-works |
| You | Face ID lock, iCloud contacts, Handoff, Focus filter, SharePlay, Wallet pass, JSON export, reset |
| Shell | iOS-style tab bar, status bar, dark mode, full-bleed on mobile, phone frame on desktop |

## What is simulated, and is not real

Be clear with anyone you show this to:

- **Apple integrations are UI only.** Sign in with Apple, Face ID, Wallet, iCloud contacts, Handoff, Focus and SharePlay are all mock interactions. None of them call a real Apple API, and all of them need a backend plus an Apple Developer account to be real.
- **No backend.** There are no accounts, no server, no message delivery. Every "member" is seeded data inside `index.html` (`PEOPLE`), and replies come from a canned array (`REPLIES`).
- **Invitation codes are not issued or verified by anything.** Any string matching the pattern `XXX-1234` gets in. Real invite issuance has to be server-side, or the whole gate is decoration.
- **No persistence beyond the browser.** Clearing site data erases everything.

## Structure

```
index.html    the entire app — markup, CSS, JS, seeded data
README.md     this file
NAMING.md     name-collision research and what it means for launch
```

## If this becomes a product

The prototype is the easy half. The parts that actually matter, roughly in order:

1. **Server-side invite issuance** — signed, single-use, rate-limited, tied to the inviter. A client-side gate is not a gate.
2. **Real Sign in with Apple** with server-side identity verification, so one person can't hold ten accounts.
3. **Moderation and reporting** — an invite-only app still needs a report path, blocking, and a response SLA. India's IT Rules 2021 grievance-officer obligations apply to intermediaries.
4. **Data protection** — under India's DPDP Act 2023, consent, purpose limitation and deletion rights all need to be designed in, not bolted on. Dating profiles are sensitive by any reading.
5. **Safety for a two-sided, high-risk product** — photo verification, no location precision, and an adult-only gate that is actually enforced.

## License

None yet. Add one before this goes public — MIT or Apache-2.0 if you want it reusable, or keep it all-rights-reserved while the name and product are unsettled.
