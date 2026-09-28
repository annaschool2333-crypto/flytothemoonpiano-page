# Agent Instructions — Fly to the Moon Piano

## Purpose

This repository contains the static website for Fly to the Moon Piano & Music Studio. Read this file before making changes so work can continue without rediscovering project decisions.

## Repository map

- `dist/` is the production website and the **only** directory that should be published.
- `dist/index.html` contains the site HTML, CSS, and JavaScript in one file.
- `dist/album/index.html` is the production album page. Navigation uses explicit `index.html` paths so both filesystem previews and Cloudflare routing work without showing a directory listing.
- `dist/assets/` contains the production photos and hero artwork. `dist/assets/album/` contains optimized WebP copies used by the album page. Certificate images must not be included in the production output.
- `album/` contains the owner's original album source photos. Keep these originals out of `dist/`; when the album changes, create optimized copies under `dist/assets/album/`, update the album markup, and redeploy.
- `docs/` contains source materials, PDFs, Word documents, and internal recommendations. Never deploy this directory publicly.
- `.openai/hosting.json` belongs to the earlier Sites hosting setup; GitHub Pages deployment should not publish it.
- No deployment workflow is currently present. The earlier draft GitHub Pages workflow was removed to prevent accidental publication while the website is unfinished.
- The site is deployed as a Cloudflare Worker named `flytothemoonpiano-page` using Workers Static Assets from `dist/`. `workers.dev` is disabled. Production is public at `https://flytothemoonpiano.com/` and `https://www.flytothemoonpiano.com/`.

## Website decisions

- The website is static; it does not require a backend for its current features.
- The album is intentionally static. Updating its photos requires optimizing/copying the new images into `dist/assets/album/`, updating `dist/album/index.html`, and redeploying. No Google Drive API integration is currently used.
- Album photos intentionally have no visible captions. Keep concise `alt` text for accessibility, but do not display it in the gallery or lightbox unless the user requests captions later.
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

- The Cloudflare Worker was published to both production custom domains on 2026-09-26 after the user approved the DNS cutover. This does not change the separate restriction against GitHub Pages.
- The GitHub account is on GitHub Free, and the repository must remain private for now.
- There is no active GitHub Pages workflow. Do not create, commit, push, or enable one until the user explicitly says the website is ready to publish.
- When publication is reconsidered, first review the final site and hosting options. If GitHub Pages is chosen, confirm repository visibility or plan eligibility and obtain explicit approval for public exposure of the personal photos.
- Any future deployment workflow must upload only `dist/`, never the entire repository.

## Custom domain and Squarespace DNS

- Intended primary domain: `www.flytothemoonpiano.com`.
- The domain is registered through Squarespace. Domain registration and DNS hosting are separate from the Cloudflare deployment.
- Squarespace changed the registrar nameservers on 2026-09-25. Public resolvers `1.1.1.1` and `8.8.8.8` now return Cloudflare's assigned nameservers (`garret.ns.cloudflare.com` and `tina.ns.cloudflare.com`), and the Cloudflare zone reports `active`, `full`, and not paused.
- On 2026-09-26 the user deleted the four imported Squarespace apex A records and the `www` CNAME to `ext-sq.squarespace.com`. `_domainconnect` and all TXT records were intentionally preserved.
- Wrangler initially deployed version `cb675379-b772-44bb-8be7-be17f2d7382a` and successfully attached Worker Custom Domains for both `flytothemoonpiano.com` and `www.flytothemoonpiano.com`. Cloudflare issued a separate certificate for each hostname.
- On 2026-09-27, version `11685f85-dc23-4b4b-8195-25395cf55541` deployed the static album page and optimized album images. Production verification confirmed HTTP 200 and the expected new content for both homepages, both `/album/` URLs, and representative WebP album assets.
- Both hostnames currently serve the same content directly; no apex-to-`www` redirect is configured.
- Keep `_domainconnect` and the existing TXT records unless a separate email/domain verification change requires otherwise.
- The local Worker preview was verified on 2026-09-25: `/` returned 200 and both production image assets returned 200. This did not create a public route.

## Verification before handoff

- Confirm all asset references under `dist/` resolve.
- Test desktop and mobile widths and check for horizontal overflow.
- Test the mobile menu, anchors, FAQ controls, and inquiry form.
- After Cloudflare deployment or domain changes, verify the production deployment, public URL, custom-domain DNS, redirect behavior, and HTTPS certificate.
- Keep temporary QA files out of the repository.

## Living-instruction requirement

This file is a living project handoff. Every agent working in this repository must update `AGENTS.md` whenever it discovers a new constraint, changes architecture or hosting, completes or blocks a deployment step, changes the production directory, modifies privacy-sensitive content, or learns anything future agents would otherwise need to rediscover. Remove stale status notes when they are no longer true, and leave the next agent with an accurate current state and clear next actions.
