# INSTRUCTIONS: how to verify business email providers with Playwright (headless, stealth)

Purpose: allow an agent (or human) to reproduce and extend the search for business email
providers that offer a free period/tier, do NOT require a phone number, and either give you
a domain out of the box (turnkey: their domains or a free custom domain) or accept BYOD.

## What to search for

1. Niche/lesser-known providers: search the web for "free custom domain email trial",
   "business email free tier", "email hosting no phone verification", regional/niche names
   (Swiss, Nordic, Canadian, German privacy providers are good hunting grounds).
2. Two distinct categories — keep them separate in results:
   - Turnkey domain: service gives you an address on THEIR domain (mail.com, Tuta, Mailum,
     eclipso freemail) or even a free custom domain at signup (Neo co.site). No BYOD needed.
   - BYOD: you must bring/own a domain, but signup itself requires no phone (Purelymail,
     Migadu, Kolab Now, DNSExit, Runbox, Postale, PolarisMail).
3. Disqualifiers to detect:
   - required phone/mobile input in the signup form (grep `input[type=tel]`, names containing
     `phone|tel|mobile|sms`, and required:true)
   - payment card required for the trial ("payment details needed for a trial")
   - service is only forwarding/anti-spam, not real mailboxes
   - trial requires purchasing a domain from the same vendor

## How to verify (Playwright, headless)

Environment notes:
- Use the system Chromium binary: `chromium.launch({ headless: true, executablePath: '/usr/local/bin/chromium', args: ['--no-sandbox'] })`
  (Playwright's bundled browsers may not be installed; the system binary always exists).
- Stealth basics for headless: realistic viewport, a common desktop user-agent, `locale: 'en-US'`,
  `--disable-blink-features=AutomationControlled`, and a random small delay (2-4s) after
  `domcontentloaded` so JS forms finish rendering. Do not rely on `networkidle` — many sites
  hang on trackers.
- Cookie/consent walls (mail.com, GMX show `/consentpage` in headless): click the accept
  button (`button:has-text("Accept")` or similar) or set the consent cookie, then reload.

Per-site procedure:
1. Load the signup/registration URL directly (find it by extracting links matching
   `/sign|register|order|trial|try|free/` from the landing page).
2. Enumerate all form controls:
   `document.querySelectorAll('input:not([type=hidden]),select')` → record
   tag, type, name/id, label (from `labels[0]`, `aria-label`, `placeholder`), and `required`.
3. Grep `document.body.innerText` for:
   - `phone|mobile|sms|telephone` — then check each hit: is it a REQUIRED input or just a
     mention/optional field? Only a required phone disqualifies.
   - `free trial|30-day|60-day|14-day|free plan|forever free|first month free` — confirms free period.
   - `custom domain|own domain|choose domain|@provider-domain` — determines turnkey vs BYOD.
4. If the form is empty after 4s, the page is JS-heavy or consent-walled: retry once with a
   consent click and 5s wait; if still empty, mark PARTIAL/unverified, do not guess.
5. Classify result: VERIFIED / PARTIAL / REJECTED, and record the exact signup URL.
6. Re-verify before trusting: provider terms change; re-run the form inspection before use.

## Output format

Keep a table per category (turnkey / BYOD / forwarding-only / rejected) with: provider,
domain policy, free period, signup fields, verification status, notes. Date every run.
