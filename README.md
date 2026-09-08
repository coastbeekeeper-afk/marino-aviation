# Marino Aviation

Professional Part 61 flight-training site for **Sam Marino, CFI**, based at **John Wayne Airport (SNA)** in Orange County, California.

**Live URL (GitHub Pages):** https://coastbeekeeper-afk.github.io/marino-aviation/

Custom domain later: `marinoaviation.com` (see below). Until Square booking exists, the primary CTA is `mailto:hello@marinoaviation.com`.

## Pages

| File | Purpose |
|---|---|
| `index.html` | Home — positioning, 6+ years, Cessna 182, rates, contact |
| `about.html` | Instructor background and who Sam takes |
| `next-steps.html` | Books, FAA medical, TSA / AFSP, video placeholders |
| `404.html` | GitHub Pages not-found |

There is no build step. GitHub Pages serves these files as-is.

## Edit the site

1. Clone this repository and work on a branch.
2. Copy is in the HTML files. Rates, email, and positioning live on `index.html`; books/medical/TSA on `next-steps.html`.
3. Photos live in `images/`. Keep filenames stable or update the `src` / `og:image` paths.
4. Shared look-and-feel is `css/styles.css`. Mobile nav is `js/nav.js`.
5. After copy changes, update:
   - `<title>` and `meta name="description"` on that page
   - Open Graph tags
   - JSON-LD in the page `<head>` if names, rates, or address change
   - `sitemap.xml` lastmod dates
6. Preview locally:

   ```bash
   python3 -m http.server 8080
   ```

   Open http://127.0.0.1:8080 — do not open files via `file://` if you care about root-relative checks; these pages use relative paths and work either way.

7. Commit, push, and merge to `main`. The Pages workflow publishes automatically.

### Photos

Place web-ready JPEGs in `images/`:

- `wing-island.jpg` — home hero (Cessna 182 wing / island aerial)
- `ramp-golden-hour.jpg` — aircraft on the ramp
- `above-clouds.jpg` — on top of a cloud layer
- `runway-lineup.jpg` — cockpit / runway
- `og-image.jpg` — 1200×630 social share image
- `favicon.svg` — browser icon

Instructor portraits from the original shoot can replace the hero or About image: drop the file into `images/` and change the corresponding `<img src>` (and alt text).

## GitHub Pages configuration

This repo deploys with **GitHub Actions** (`.github/workflows/pages.yml`).

1. **Settings → Pages**
   - Source: **GitHub Actions**
   - The workflow calls `actions/configure-pages` with `enablement: true`, which turns Pages on for this public repo if it is not already enabled. The first successful run publishes the site.
2. Workflow triggers:
   - Push to `main` (production)
   - Push to `cursor/marino-aviation-site-f357` (initial publish from this work)
   - Manual **Run workflow**
3. Public URL:

   `https://<owner>.github.io/marino-aviation/`

   For this repository that is:

   **https://coastbeekeeper-afk.github.io/marino-aviation/**

`.nojekyll` is present so GitHub does not run Jekyll on the static files.

If a deploy fails with “GitHub Pages is not enabled,” open **Settings → Pages**, choose **GitHub Actions** as the source, and re-run the workflow.

After the custom domain is live, you can drop the extra feature-branch trigger from the workflow and keep `main` only.

## Point marinoaviation.com at this site

GitHub Pages supports a custom apex (and `www`) domain.

1. In the repo, add a `CNAME` file at the root containing only:

   ```
   marinoaviation.com
   ```

2. In **Settings → Pages → Custom domain**, enter `marinoaviation.com` and save. Enable **Enforce HTTPS** once the certificate provisions.

3. At your DNS host, create:

   | Type | Name | Value |
   |---|---|---|
   | `A` | `@` | `185.199.108.153` |
   | `A` | `@` | `185.199.109.153` |
   | `A` | `@` | `185.199.110.153` |
   | `A` | `@` | `185.199.111.153` |
   | `AAAA` | `@` | `2606:50c0:8000::153` |
   | `AAAA` | `@` | `2606:50c0:8001::153` |
   | `AAAA` | `@` | `2606:50c0:8002::153` |
   | `AAAA` | `@` | `2606:50c0:8003::153` |
   | `CNAME` | `www` | `coastbeekeeper-afk.github.io` |

   GitHub’s current Pages IPs are documented at [Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

4. Replace every `https://coastbeekeeper-afk.github.io/marino-aviation` URL in:

   - `index.html`, `about.html`, `next-steps.html` (`link rel="canonical"`, Open Graph, JSON-LD)
   - `sitemap.xml`
   - `robots.txt`

   with `https://marinoaviation.com` (no `/marino-aviation` path).

5. Push to `main` and wait for DNS + TLS (often 15–60 minutes; sometimes longer).

Do **not** add the `CNAME` file until DNS is ready to follow; an unmatched CNAME can break the `github.io` URL.

## SEO notes

- Titles and H1s target: flight instructor Orange County, CFI at John Wayne Airport / SNA, Part 61.
- Copy may describe Sam as among Orange County’s strongest CFIs / a top choice for serious students. Do not add fake awards, rankings, or “#1 certified by …” claims.
- `LocalBusiness` + `FlightSchool` JSON-LD uses the SNA / Santa Ana address area.
- Keep identifier casing and claims consistent with reality when you edit.

## Contact and rates (source of truth)

- Email: hello@marinoaviation.com
- Flight: $295/hour flat (instruction + fuel + aircraft)
- Ground: $55/hour
- Deposit required; free cancel up to 24 hours before
