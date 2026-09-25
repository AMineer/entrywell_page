# Entrywell website

A complete static website for entrywell.app. No npm, frameworks, build step, API keys, backend, or tracking scripts. All assets are local. The responsive pages work without JavaScript.

## Included pages

| URL | Purpose |
| --- | --- |
| `/` | Product landing page with interface concept, benefits, plans, and FAQ |
| `/marketing/` | Dedicated marketing page with audiences and the planned product workflow |
| `/support/` | Contact information and support questions |
| `/privacy/` | Current website notice and planned app privacy approach |
| `/terms/` | Prelaunch terms, planned subscriptions, and Apple Standard EULA link |
| `/404.html` | Custom missing-page screen |

The website is deliberately in **prelaunch mode**. It contains no invented App Store URL, testimonials, customer counts, or performance claims. The phone is an HTML/CSS design preview with sample data, not a screenshot or interactive app. The small text within that illustration is decorative preview content; explanatory text is outside the illustration.

## Publish through GitHub Pages

1. Create a new repository, for example `entrywell-site`. A public repository works with GitHub Free. If using a private repository, verify your GitHub plan supports Pages.
2. Put this package's **contents** at the repository root. `docs/index.html` must be directly inside the root's `docs` folder. Do not add an extra nested `entrywell-site` folder.
3. Push or upload the files to the `main` branch. Include `docs/.nojekyll` and `docs/CNAME`. On a Mac, use Command-Shift-Period to reveal hidden files if uploading through the browser.
4. In **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, then **main** and **/docs**. Save.
5. In **Settings → Pages → Custom domain**, enter **entrywell.app** and save. The supplied `docs/CNAME` contains the same domain.
6. Configure DNS as described below. Once the certificate is available, enable **Enforce HTTPS**.

No custom Actions workflow is required. GitHub handles the branch-based publishing workflow. Future commits to `main` update the site. This package has not been uploaded to a GitHub account or deployed.

## DNS for entrywell.app

Configure records at the domain's active DNS provider. If GoDaddy manages its nameservers, use GoDaddy's DNS management screen.

| Type | Host | Value |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |
| CNAME | www | YOUR-GITHUB-USERNAME.github.io |

Replace `YOUR-GITHUB-USERNAME` with the personal or organization account owning the repository. Do not include the repository name in the CNAME target. If your DNS provider supports ALIAS/ANAME at the root, GitHub also documents that as an alternative to the apex address records.

Remove conflicting **website** records or forwarding for `@` and `www`; preserve unrelated email MX/TXT records. Do not use wildcard DNS. Consider verifying the domain in your GitHub account's Pages settings using the TXT record GitHub supplies.

Certificate provisioning can take time. If HTTPS is pending, inspect the DNS records and GitHub Pages status rather than repeatedly changing them.

Official setup references, consulted September 24, 2026:
- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https
- https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages

## Preview locally on your Mac

From this folder:

```sh
python3 -m http.server 8080 --directory docs
```

Open http://localhost:8080. Press Control-C to stop. A local server gives accurate directory-route behavior. The custom 404's links deliberately point to the production domain so they work even for nested missing URLs.

## Brand and editing

- Shared styles and responsive behavior: `docs/assets/styles.css`
- Generated paper-E brand asset: `docs/assets/entrywell-icon.png`
- Small simple vector favicon: `docs/assets/favicon.svg`
- Colors: ink `#243B53`, paper `#F7F4ED`, blue `#356A9A`, brass `#C49A57`, secondary text `#526378`
- Fonts: operating-system sans serif plus Georgia for large editorial headings; no external font requests.
- Browser color scheme is intentionally light. The app concept retains the navy/ivory brand.
- Headers and footers are static HTML in each page. Update all five pages when changing shared navigation.

## Before publishing

Support and terms inquiries use **support@a2m4systems.com**. Privacy inquiries use **privacy@a2m4systems.com**. Both visible addresses and email links use these business mailboxes.

Pricing and features reflect the supplied Phase 1 build specification, not a verified release. Keep the prelaunch labels until you are ready to launch. Confirm the Free/Pro split and final StoreKit pricing.

The privacy and terms pages are tailored prelaunch drafts. Review them against actual app behavior and business practices before using them as final App Store disclosures. In particular, confirm diagnostic data, receipt processing, iCloud behavior, sharing permissions, deletion, support email retention, and whether any SDKs or analytics are added. The website notice distinguishes GitHub's security logging from app data handling. This package does not provide a legal clearance or claim a policy meets every jurisdiction's requirements.

Relevant source references:
- GitHub Pages security logging: https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages
- Apple Standard EULA: https://www.apple.com/legal/internet-services/itunes/dev/stdeula/
- Apple subscription management: https://support.apple.com/118428

## When the app launches

1. Add the verified App Store URL to the primary calls to action on `docs/index.html` and `docs/marketing/index.html`.
2. Replace “in development” wording and the availability FAQ with confirmed release information.
3. Replace the design preview with actual release screenshots if desired. Do not describe it as a screenshot until you do.
4. Confirm support guidance, the privacy notice, subscription terms, device requirements, and shipping features.
5. Keep the domain and URL paths unchanged. Use these URLs in App Store Connect:
   - Marketing: `https://entrywell.app/marketing/`
   - Support: `https://entrywell.app/support/`
   - Privacy: `https://entrywell.app/privacy/`
   - Terms: `https://entrywell.app/terms/`

## Validation performed

- All six HTML documents have a title, description, main landmark, and primary heading.
- Local links, images, and fragment targets resolve.
- Five public routes, the custom 404, stylesheet, icon, favicon, sitemap, and robots file return HTTP 200 from the local static server.
- Sitemap XML parses; custom domain and `.nojekyll` configuration are present.
- Responsive layouts include narrow-screen rules and reduced-motion support.
- Browser visual and interaction testing could not run in the build environment because the Chromium download failed. Preview on desktop and iPhone before publishing.
