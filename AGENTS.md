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
- This fork uses GitHub Pages branch deployment from `gh-pages`; there is no custom workflow.
- The upstream site uses Cloudflare. This fork is published independently through GitHub Pages as described below.

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

- Fork: `https://github.com/annaschool2333-crypto/flytothemoonpiano-page`
- Default source branch: `main`; this fork is public.
- On 2026-11-02 the owner explicitly requested publication of this fork through GitHub Pages using GitHub CLI. This supersedes the inherited upstream restrictions on Pages publication.
- GitHub Pages publishes only the contents of `dist/`, copied as the root tree of the `gh-pages` branch.
- Public URL: `https://annaschool2333-crypto.github.io/flytothemoonpiano-page/`
- This is a snapshot deployment. Future edits to `main/dist` require updating `gh-pages` to the new `dist` tree; they do not deploy automatically.
- Do not publish `docs/`, raw `album/` originals, certificates, or `.openai/`.
- Preserve relative asset and navigation paths for the repository subpath.
- The existing upstream Cloudflare custom domains and DNS are separate; do not change them for this fork.
- No GitHub Actions workflow was added. Branch publishing works with the current CLI authorization.

## Historical upstream custom domain and Squarespace DNS

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

## Fork custom domain — 2026-11-02

- The owner authorized connecting flytothemoonpiano.com to this fork's GitHub Pages site, superseding the earlier instruction to leave domain DNS unchanged.
- Pages custom domain: www.flytothemoonpiano.com. GitHub created CNAME on gh-pages; retain this file in future snapshot deployments.
- Squarespace registrar nameservers were switched from garret.ns.cloudflare.com / tina.ns.cloudflare.com to nsc1 through nsc4.squarespacedns.com.
- Squarespace website default preset was replaced. DNS now uses @ ALIAS annaschool2333-crypto.github.io and www CNAME annaschool2333-crypto.github.io.
- Domain Connect and all three Email Security TXT records were preserved.
- Public DNS resolves to GitHub Pages; www HTTP returned 200. HTTPS certificate issuance was still pending at handoff. Enable Pages HTTPS enforcement once its certificate is ready, then verify HTTPS on apex, www, and album.
