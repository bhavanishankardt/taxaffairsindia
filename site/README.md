# Tax Affairs — Website

A Jekyll site built for free hosting on GitHub Pages. The design is
deliberately restrained and editorial — a quiet numbered list for
practice areas, hairline rules, and a single red accent used only as
a section marker, rather than a boxed "template" look. Palette: navy
(#032058), red (#CA090A), true black (#0B0C10) for the footer, and
white throughout. GitHub Pages builds Jekyll sites automatically —
you don't need to run any build step yourself; you just push files
and turn a setting on.

The site is framed as a consultancy (Advisory · Compliance ·
Litigation) rather than a personal CA practice — there's no ICAI
membership number or "Chartered Accountant practice" language
anywhere on it. It now covers 25 towns across Andhra Pradesh, grouped
by region (Rayalaseema / Coastal Andhra) on the homepage.

## 1. Before you push anything — fill in your real details

Open `_config.yml` and replace these three placeholder lines:

```yaml
phone: "+91-XXXXXXXXXX"
whatsapp: "91XXXXXXXXXX"     # digits only, no +, no spaces — used in wa.me links
email: "contact@taxaffairsindia.in"
```

Every page pulls these from `_config.yml` automatically — you only edit them once, here.

## 2. Put it on GitHub

1. Create a new **public** repository on GitHub, e.g. `taxaffairsindia-site`.
2. Upload every file in this folder to that repository (drag-and-drop on
   github.com works fine for a first pass, or `git push` if you're
   comfortable with git).
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment", set **Source** to "Deploy from a branch",
   pick the `main` branch and `/ (root)` folder, then **Save**.
5. GitHub will build the site (takes 1–2 minutes) and give you a URL like
   `https://yourusername.github.io/taxaffairsindia-site/`. Open it to
   confirm the site looks right before moving to your own domain.

## 3. Point taxaffairsindia.in at it

Since you already own the domain:

1. Still in **Settings → Pages**, under "Custom domain", type
   `taxaffairsindia.in` and save. GitHub will create a `CNAME` file in
   your repo automatically.
2. Go to wherever you bought the domain (GoDaddy, Namecheap, etc.) and
   open its DNS settings. Add:
   - Four **A records** for the root domain (`@`), pointing to:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - One **CNAME record** for `www`, pointing to `yourusername.github.io`
3. DNS changes can take anywhere from a few minutes to a few hours to
   take effect. Once they do, tick "Enforce HTTPS" back in the GitHub
   Pages settings for a free SSL certificate.

## 4. Make the contact form actually send you enquiries

`contact.html` has a form, but GitHub Pages only serves static files —
it can't process form submissions on its own. The quickest fix:

1. Create a free account at [formspree.io](https://formspree.io).
2. Create a new form there; it gives you an endpoint like
   `https://formspree.io/f/abc12345`.
3. In `contact.html`, replace `action="#"` with that endpoint.

Until you do this, use the phone/WhatsApp/email details next to the form.

## 5. Editing content later

- **Prices, service descriptions**: edit the relevant file directly —
  `index.html` for the homepage summary, or the matching file in
  `services/`. Each price row is one `<div class="folio-row">` block.
- **Add a new town/district page**: copy any file in `locations/`,
  rename it `best-tax-consultant-<town>.html`, and update the front
  matter (`title`, `description`, `keywords`, `geo_lat`, `geo_lng`,
  `geo_name`) and the visible town name in the body. Then add the town
  to `_data/towns.yml` so it shows up in the homepage grid and footer
  automatically.
- **Header/footer/contact details**: edit `_includes/header.html`,
  `_includes/footer.html`, or `_config.yml` — these changes apply to
  every page at once.
- **Colours/fonts**: all in `assets/css/style.css`, under the
  `:root { ... }` block at the top for colours.

## 6. A note on the prices shown

The starting prices on the site (₹999 for a salaried ITR, ₹1,999 for
GST registration, and so on) are illustrative placeholders in the
tax2profit.com style you asked for — **not** your actual fee schedule.
Check every price against what you actually want to charge before the
site goes live; accounting & bookkeeping is deliberately left as
"reasonable charges — contact us" rather than a fixed number, as you
asked.

## 7. Getting found on Google — what the site handles vs. what you still need to do

The site itself now carries everything on-page SEO can offer:
- Unique title/description/keywords per page, geo-coordinates per town, a canonical URL on every page, and a sitemap.xml generated automatically by the `jekyll-sitemap` plugin
- `ProfessionalService` and `FAQPage` structured data (JSON-LD) so Google can understand what the business is and surface FAQ answers directly in search results
- A logo, Open Graph and Twitter Card tags for clean previews when the site is shared

None of that guarantees ranking on its own — visibility mostly comes from things outside the site's code:
1. **Google Business Profile** — create one (free, at business.google.com) for "Tax Affairs" with your Proddatur address. This is what actually gets you into Google's local map pack for "tax consultant near me" searches — arguably the single highest-impact thing you can do.
2. **Google Search Console** — verify the domain and submit `https://taxaffairsindia.in/sitemap.xml` so Google knows to crawl every page, including the town pages.
3. **Backlinks** — get listed on local business directories (Justdial, Sulekha, IndiaMART), and if you're a member of any local trade/chamber body, ask for a website link there.
4. **Genuine client reviews** on your Google Business Profile — these matter more for local ranking than almost anything on the site itself. Never fabricate these.
5. **Ongoing content** — a simple blog/updates page (e.g. "GST due dates this month," "New ITR forms for AY 2027-28") gives Google fresh content to re-crawl and gives you more long-tail keyword pages over time.

## File structure

```
_config.yml          site-wide settings (firm name, contact details)
_data/towns.yml       list of AP towns/districts shown across the site
_layouts/default.html the shared page shell (head, header, footer)
_includes/            header.html, footer.html
assets/css/style.css  all styling
index.html             homepage
about.html, contact.html
services/              one page per service line
locations/             one SEO landing page per AP town
robots.txt, 404.html, Gemfile
```
