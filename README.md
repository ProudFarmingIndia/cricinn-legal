# CricInn — legal & support pages

Four static pages for GitHub Pages. No build step, no dependencies.
Published at **https://cricin.app/**

    index.html            hub, links to all three
    privacy.html          Privacy Policy
    terms.html            Terms of Use
    delete-account.html   account deletion (Play requires this URL)
    style.css             shared stylesheet

Everything is already filled in — brand **CricInn**, contact
**support@cricin.app**, operator **Gagan Choudhary**, jurisdiction
**Ghaziabad, Uttar Pradesh**, dated **12 November 2026**.

Check two things before publishing:
- `Gagan Choudhary` must match the legal name on your Play Console account exactly.
- `support@cricin.app` must be a mailbox you actually read. Google tests it.

Note: the app is called **CricInn** and the domain is **cricin.app** — one `n`
in the domain, two in the name. That is deliberate; keep it consistent
everywhere rather than "fixing" one of them later.

The public contact address everywhere is **support@cricin.app** — the Gmail
account that owns the developer accounts is a separate, private thing and
should never appear on the store listing or in these pages.

---

## 1. Put it on GitHub Pages

1. New **public** repo on GitHub, name it `cricinn-legal`.
2. Upload these five files to the root (*Add file → Upload files*, drag and drop).
3. **Settings → Pages → Source: Deploy from a branch → Branch `main`, folder `/ (root)` → Save**.
4. Still on that page, set **Custom domain** to `cricin.app`. GitHub shows the exact
   DNS records to add — copy those into your registrar.
5. Once the check passes, tick **Enforce HTTPS**.

> ### `.app` requires HTTPS — this is not optional
>
> The whole `.app` top-level domain sits on the browsers' HSTS preload list, so
> Chrome, Edge, Brave and Safari **refuse to load a `.app` site over plain
> HTTP** — not a warning, a hard refusal.
>
> In practice: after you point DNS at GitHub Pages there is a gap of a few
> minutes to about an hour while GitHub provisions the TLS certificate. During
> that gap `https://cricin.app` simply will not load, and it will look like the
> whole thing is broken. It is not. Wait for **Enforce HTTPS** to become
> tickable, tick it, then test.
>
> **Do not submit the privacy policy URL to Play Console until `https://cricin.app/privacy.html`
> opens cleanly in a browser.** Google fetches it, and a failed fetch is a
> rejection.
>
> Email is unaffected — HSTS is a web-only rule, so Zoho MX records work
> normally.
6. Point `cricin.com` at `cricin.app` with a registrar-level redirect, so the
   older domain does not dead-end.

Final URLs:

    https://cricin.app/
    https://cricin.app/privacy.html
    https://cricin.app/terms.html
    https://cricin.app/delete-account.html

**Never change these paths.** Once a URL is submitted to Play Console it has to
keep working — when you build a real website later, keep these three files where
they are.

---

## 2. Where each URL goes in Play Console

| URL | Play Console location |
|---|---|
| `https://cricin.app/privacy.html` | **App content → Privacy policy**, and again in **Store listing** |
| `https://cricin.app/delete-account.html` | **App content → Data safety → Data deletion**, as the web link where users request deletion |
| `https://cricin.app/terms.html` | Not required by Play. Link it from inside the app next to the privacy policy. |

---

## 3. Still to build in the app itself

These pages *describe* behaviour that must actually exist. Google checks.

- **Settings → Delete my account** — in-app deletion. The web URL alone is not
  enough; Google requires both.
- On deletion: wipe the account and profile, but **anonymise** the player in
  existing balls and scorecards rather than deleting them, or every other
  player's statistics break.
- **Report and block** on profiles and gallery photos — `terms.html` section 6
  promises it.
- **Terms acceptance gate** at signup, and re-acceptance when the version number
  changes. Store `acceptedTermsVersion` on the user.
- **18+ check** at signup, using the `dob` field the profile already has.

---

## 4. When you change the text later

Bump the version number and the date at the top of the page you changed, and
make the app ask users to accept again.
