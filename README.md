# Business Email Services — verified free/trial providers (turnkey domain + BYOD)

Verified with headless Chromium (Playwright) on 2026-10-25 by live inspection of signup forms.
Criteria: service exists, free period or free tier, no mandatory phone number, signup via email (or Google), ideally obscure providers.

Status legend:
- ✅ VERIFIED — signup form inspected live, no required phone field
- 🟡 PARTIAL — service confirmed, full signup flow not completed (JS/consent walls)

## A. Turnkey domain included (no BYOD needed)

| Provider | Domain given | Free period | Signup | Status | Notes |
|---|---|---|---|---|---|
| Neo (neo.space) | Free co.site domain at signup | 15-day trial | Full name + email only, no phone | ✅ | Free domain provided if you don't own one; business email + free AI website |
| mail.com | 100+ professional domains (e.g. @consultant.com, @engineer.com) via "Choose domain" select | Free forever | Username + password form, no phone field on signup page | ✅ | Owned by 1&1; recovery email optional |
| Mailum (mailum.com) | @mailum.com | Free tier (1 address, 0.05GB) | Email-based, site states "no phone verifications" | 🟡 | Premium upgrade free for 7 days; own domain only on paid |
| Tuta (app.tuta.com/signup) | @tuta.com / @tutamail.com / @tutanota.com | Free tier | Email-based, no phone field | 🟡 | Free plan is small; paid plans for business use |
| Mailfence (mailfence.com) | @mailfence.com | Free plan | Email-based, no phone hits on page | 🟡 | Free plan is minimal; own domain requires paid plan |
| eclipso.eu | freemail domains (@maileurope.de, .at, .ch, .es, .fr, .co.uk, .it, .nl) | Free | "no phone number, no personal information" per official page | 🟡 | Signup form is JS-rendered; freemail is free, own domain is paid |

## B. BYOD required (bring your own domain) — free period, no phone

| Provider | Free period | Signup | Status | Notes |
|---|---|---|---|---|
| Purelymail (purelymail.com/signup) | Free trial, no card (then $10/yr) | Username, password, optional recovery email; radio "Start a free trial" | ✅ | Unlimited domains/users; phone only as optional recovery |
| Migadu (admin.migadu.com/public/signup) | Free trial, no card | Name, email, TOS only | ✅ | Swiss, niche; BYOD required |
| Kolab Now (kolabnow.com/signup) | 30 days free | Name + existing email + email confirmation code; checkbox "Use your own domain" | ✅ | Swiss, niche |
| DNSExit (dnsexit.com/users/signup) | Free forever (2 mailboxes, 100MB) | Username, password, email + simple captcha | ✅ | Also offers free second-level domains |
| Runbox (runbox.com/app/signup?runbox7=1) | 30 days, no credit card | Name, username, "Use my own domain" selector, email required | ✅ | Phone fields present but marked Optional; Norwegian |
| Postale.io (postale.io/pricing) | Free 30-day trial | Domain email + contact email | ✅ | Small US provider |
| PolarisMail (billing.emailarray.com/register) | 30-day free trial | Radio "My own domain" or "@polarismail.net (ready instantly)" | ✅ | Canadian, since 2008; phone field exists but required:false |
| Fastmail (app.fastmail.com/signup) | Up to 30 days, no card | Name, "Use your own domain" checkbox, password | ✅ | Known brand; help docs say SMS verification may be requested for spam prevention |
| Infomaniak kSuite Standard (infomaniak.com) | Free tier incl. custom domain | Email-based | 🟡 | Swiss; kSuite Standard free tier includes custom domain per FAQ/community |
| mailbox.org | 30-day free trial | Multi-step JS flow (not fully completed by bot) | 🟡 | German; no phone required |

## C. Free forwarding only (no mailboxes)

| Provider | Free | Signup | Status |
|---|---|---|---|
| ForwardEmail (forwardemail.net/en/register) | Free forever, forwarding only, unlimited domains | Email+password or Google/GitHub/Apple OAuth | ✅ |

## D. Checked and rejected (do not retry without reason)

- MX Guarddog — anti-spam gateway for an existing mail server, NOT mailbox hosting (first month free, no phone, but no mailboxes)
- Mailum free tier — no own domain support (BYOD paid only)
- Stalwart — 30-day trial is for a self-hosted license, not a hosted service
- StartMail — trial requires payment details
- Soverin — 30-day money-back guarantee only, no free trial
- Mailfence own domain — paid plans only
- dismail.de — free donation-based email, signup form did not render headless; own domain unconfirmed
- mail.rs — domain does not resolve (dead/unreachable)
- Dynadot Email — free only with a domain purchased at Dynadot
- eclipso BYOD — own domain is a paid feature (freemail domains are free, see section A)
- Namecheap Private Email — 60-day trial requires a domain purchased at Namecheap
- Greatmail / Mailo — signup forms did not render headless (unverified)

## Method

All results were obtained by loading each signup page in headless Chromium via Playwright,
enumerating `input`/`select` elements with name/type/required flags, and grepping page text
for phone/SMS mentions and free-trial wording. See INSTRUCTIONS.md for the full procedure.
