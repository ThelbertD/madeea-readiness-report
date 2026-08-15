# MadeEA — Readiness Review

One report covering two tracks of MadeEA work, and the defect they turn out to
share.

**Part one — MadeEA OS on a custom domain.** The gateway needed to put the OS on
a domain is already built and tested (`omniroute-team-hub`: 83 passing tests,
per-user quotas, JWT auth, OmniRoute bound to loopback). The 246-route Next.js
app around it is not safe to expose — 33 routes spawn CLIs on the host and 15
check authorization. The published static export also still points at a
Cloudflare quick tunnel that no longer exists.

**Part two — the DM setter across social platforms.** Sending is already
channel-agnostic: Instagram appears in exactly two places, a filter line and a
`type` constant, on an endpoint that also carries Messenger, WhatsApp and SMS.
Facebook Messenger is the cheapest next channel. LinkedIn and TikTok have no
public messaging API and are closed regardless of effort.

**Both tracks.** The same duplication bug in two unrelated systems — the browser
shim exists in two copies, the SOP prompt in three — and neither fails loudly.

Every count was measured against the files in `For Work/MadeEA OS` and
`MadeEA Hub new/n8n/`, not estimated.

## Deploying

Plain static HTML — no build step, no framework, no dependencies.

- **Vercel:** import this repo at [vercel.com/new](https://vercel.com/new). Leave
  every build setting empty; `index.html` at the root is the whole site.
- **GitHub Pages:** Settings → Pages → deploy from `main`, root folder.
- **Anywhere else:** upload `index.html`. That's it.

## Updating

Edit `index.html` directly. Styles are inline and both light and dark themes are
defined through CSS custom properties — change a token in `:root` and both
themes follow. The stylesheet is shared with the other MadeEA report pages, plus
a `.part` block for the two part dividers.

Platform access rules change. The verdicts in part two are stable; the window
rules, API tiers and rate cards behind them should be re-checked at the moment a
channel is committed to.

## Contents

| File | |
|---|---|
| `index.html` | The report, self-contained |
