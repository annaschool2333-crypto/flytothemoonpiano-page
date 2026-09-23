# Agent Instructions — Fly to the Moon Piano

## Purpose

This repository contains the static website for Fly to the Moon Piano & Music Studio. Read this file before making changes so work can continue without rediscovering project decisions.

## Repository map

- `dist/` is the production website and the **only** directory that should be published.
- `dist/index.html` contains the site HTML, CSS, and JavaScript in one file.
- `dist/assets/` contains the production photos and hero artwork. Certificate images must not be included in the production output.
- `docs/` contains source materials, PDFs, Word documents, and internal recommendations. Never deploy this directory publicly.
- `.openai/hosting.json` belongs to the earlier Sites hosting setup; GitHub Pages deployment should not publish it.
- No deployment workflow is currently present. The earlier draft GitHub Pages workflow was removed to prevent accidental publication while the website is unfinished.
- The user reports that the site has now been deployed manually to Cloudflare. The exact Cloudflare product (`*.pages.dev` versus `*.workers.dev`), project name, production URL, and Git integration status have not yet been verified.

## Website decisions

- The website is static; it does not require a backend for its current features.
- The Book a Trial section uses a website-styled CTA button that opens the official public Google Form in a new tab. Do not embed the form in an iframe unless the user explicitly changes this decision.
- Official inquiry form URL: `https://docs.google.com/forms/d/e/1FAIpQLSc6c9_bHG8ZmEys1GOgaVO02bmRHWofc457C0pebnBd2_wlbQ/viewform`.
- Official public contact email: `moonlovemelody520@gmail.com`. Keep it available as a clickable `mailto:` link in the Book a Trial section and footer; the Google Form remains the primary inquiry path.
- The credential section intentionally emphasizes one primary qualification: Nationally Certified Teacher of Music in Piano.
- Other education and coursework should remain concise text so they support the teaching story without being presented as equivalent professional music credentials.
- The user explicitly chose not to display certificate scans on the website. Present qualifications as text with restrained inline SVG icons; keep original certificate files only in internal `docs/` source materials.
- Do not expose exact home/studio directions. Public location copy should remain limited to Renton, WA 98059 and nearby service areas.
- Preserve accessibility, responsive behavior, reduced-motion support, working mobile navigation, and relative asset paths.

## Git and GitHub

- Repository: `https://github.com/paulpowang/flytothemoonpiano-page.git`
- Default branch: `main`
- Git identity: `PoHung Wang <wang.po.hung@gmail.com>`
- GitHub CLI is installed at `C:\Users\wangp\AppData\Local\Programs\GitHub CLI\2.101.0\bin\gh.exe`.
- GitHub CLI authentication is separate from Git Credential Manager. Check `gh auth status` before using GitHub APIs.
- The exact repository path has been added to Git `safe.directory` because the working copy was created under a different sandbox identity.
- Keep the repository private unless the user explicitly approves changing its visibility.

## Publication and privacy guardrails

- GitHub Pages publishes a publicly accessible website even when its source repository is private.
- The production output includes Anna's personal photos. The user has already chosen to deploy the site through Cloudflare; do not move it to another host or expose internal `docs/` materials.
- The owner's personal GitHub account is currently on GitHub Free. Keep the repository private and do not attempt GitHub Pages from this repository unless the user later changes plans, upgrades, explicitly makes the repository public, or selects another host.
- Never publish `docs/`, source certificates, internal recommendations, or raw reference materials.
- Never request or store the user's GitHub or Squarespace password. For web-account changes, ask the user to sign in and share/mention the authenticated browser tab.

## GitHub Pages status

- The user has explicitly decided not to publish yet because the website is unfinished.
- The GitHub account is on GitHub Free, and the repository must remain private for now.
- There is no active GitHub Pages workflow. Do not create, commit, push, or enable one until the user explicitly says the website is ready to publish.
- When publication is reconsidered, first review the final site and hosting options. If GitHub Pages is chosen, confirm repository visibility or plan eligibility and obtain explicit approval for public exposure of the personal photos.
- Any future deployment workflow must upload only `dist/`, never the entire repository.

## Custom domain and Squarespace DNS

- Intended primary domain: `www.flytothemoonpiano.com`.
- The domain is registered through Squarespace. Domain registration and DNS hosting are separate from the Cloudflare deployment.
- Current DNS still points to Squarespace:
  - `www` CNAME → `ext-sq.squarespace.com`
  - Apex A records → Squarespace IP addresses
- Do not change Squarespace DNS until the exact Cloudflare production hostname and deployment type are confirmed.
- If this is Cloudflare Pages, add `www.flytothemoonpiano.com` under the Pages project's Custom domains first, then set the Squarespace `www` CNAME to the project's exact `<project>.pages.dev` hostname. A manually created CNAME without first associating the custom domain can fail.
- If this is a Cloudflare Worker custom domain, the domain must be an active Cloudflare zone; do not assume the Pages CNAME procedure applies.
- Connecting the apex domain `flytothemoonpiano.com` directly to Cloudflare Pages requires delegating nameservers to Cloudflare. A `www` subdomain can remain on external Squarespace DNS using CNAME.
- DNS changes can interrupt the current Squarespace destination. Verify the Cloudflare deployment first, make exact DNS changes, then validate `www`, apex redirect behavior, and HTTPS.

## Verification before handoff

- Confirm all asset references under `dist/` resolve.
- Test desktop and mobile widths and check for horizontal overflow.
- Test the mobile menu, anchors, FAQ controls, and inquiry form.
- After Cloudflare deployment or domain changes, verify the production deployment, public URL, custom-domain DNS, redirect behavior, and HTTPS certificate.
- Keep temporary QA files out of the repository.

## Living-instruction requirement

This file is a living project handoff. Every agent working in this repository must update `AGENTS.md` whenever it discovers a new constraint, changes architecture or hosting, completes or blocks a deployment step, changes the production directory, modifies privacy-sensitive content, or learns anything future agents would otherwise need to rediscover. Remove stale status notes when they are no longer true, and leave the next agent with an accurate current state and clear next actions.
