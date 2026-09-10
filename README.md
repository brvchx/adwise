# AdWise — support, privacy and terms

Three static pages linked from App Store Connect. Plain HTML and CSS, nothing to build
and nothing to maintain.

```
index.html     Support page      → App Store Connect "Support URL"
privacy.html   Privacy Policy    → App Store Connect "Privacy Policy URL"
terms.html     Terms of Use      → App Store Connect "License Agreement"
style.css      Styling, light and dark theme
```

## Why self-hosted

The app was removed under App Review Guideline 1.5 because the domain in the Support URL
field stopped responding. The privacy policy used to live on a third-party generator
site — the same risk: someone else's service, someone else's account, someone else's
uptime. Hosting the pages ourselves removes that whole class of failure.

## Deploying

**1. Enable Pages.** Repository → Settings → Pages → Source: **Deploy from a branch** →
Branch `main`, folder `/ (root)` → Save. The address appears at the top after a minute
or two.

> GitHub Pages only serves from a **public** repository on the free plan. If the
> repository is private, Pages is switched off and the links stop working. Either keep
> the repository public, upgrade to GitHub Pro, or host the same files on Cloudflare
> Pages or Netlify, both of which serve public sites from private repositories for free.

**2. Verify.** Open all three URLs and check that they load and link to each other.

**3. Fill in App Store Connect.**

| Field | Where in ASC | URL |
|---|---|---|
| Support URL | App version page | `.../` |
| Privacy Policy URL | App Information → App Privacy | `.../privacy.html` |
| License Agreement | App Information → License Agreement → Custom | `.../terms.html` |

**4. Keep the app in sync.** `Constants.swift` in the iOS project points at these same
pages. If the addresses change, update it there too.

## Things to check before shipping

- **The email address** `adblockdev@outlook.com` appears on all three pages. Make sure
  somebody actually reads that mailbox — an App Review specialist may write to it. A dead
  support address is exactly what caused the 1.5 removal.
- **The promised response time** on the support page is 48 hours. Only promise what can
  be met.
- **Jurisdiction** in the Terms is Latvia, matching where ASKOR SIA is registered.

## What the texts already cover

The privacy policy is written against the specific rules that cause rejections:

- **Guideline 5.4 (VPN apps)** — states plainly what is collected on connection, that no
  connection logs are kept, and that data is never sold or shared. VPN apps do not pass
  review without this.
- **Guideline 3.1.2** — auto-renewing subscriptions, cancellation and refunds.
- **Tracking and IDFA** — describes the ATT prompt and confirms the app works identically
  if tracking is declined.
- **Processor list** — Firebase, AppsFlyer, Apphud, Branch, Apple, DigitalOcean, each
  with a link to its own policy. This list must match the App Privacy questionnaire in
  App Store Connect exactly.
- **GDPR** — user rights and how to exercise them.

Yandex Metrica was removed from the app, so it is not listed. Branch, AppsFlyer and
Apphud remain and are listed in section 7 and in the data table.
