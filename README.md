# Fall Line Auto Detailing — Website

A complete, static (HTML/CSS/JS only — no build step, no dependencies) 15-page
website, built mobile-first for a mobile detailing business serving the
Richmond, VA metro area.

## 1. Preview it right now

Just double-click `index.html` (or any other page) — it opens directly in
your browser, no server needed. All internal links and images work relative
to the file structure, so keep the folders together as-is.

## 2. What's in here

```
index.html            Home
about.html
reviews.html
contact.html          Booking / quote form
services/
  full-detail.html
  standard-detail.html
  interior-deep-clean.html
  ceramic-coating.html
areas/                One page per service-area city (unique copy on each,
  richmond.html        for local SEO — not duplicated text)
  chesterfield.html
  midlothian.html
  colonial-heights.html
  chester.html
  glen-allen.html
  short-pump.html
css/style.css          All design/styling — one file, no framework
js/main.js             Mobile nav, before/after slider, form handling
images/README.txt      Exact filenames the site expects — drop your photos in
```

## 3. Before you launch — placeholders to replace

**Phone number & email** — every page currently uses a placeholder number
`(804) 555-0142` (as text, `tel:+18045550142`, and `sms:+18045550142`) and
`info@falllineautodetailing.com`. Once you have a real business number,
replace it everywhere in one shot:

```powershell
# Run from the project folder in PowerShell — updates every file at once.
Get-ChildItem -Recurse -Include *.html,*.js | ForEach-Object {
  (Get-Content $_.FullName -Raw) `
    -replace '\(804\) 555-0142', '(YOUR) NEW-NUMBER' `
    -replace '\+18045550142', '+1YOURNEWNUMBER' `
    -replace 'info@falllineautodetailing\.com', 'your-real-email@example.com' |
    Set-Content $_.FullName -NoNewline
}
```
Use the same digits-only format (`+1XXXXXXXXXX`) for the `tel:`/`sms:` version
so click-to-call and click-to-text work correctly.

**Images** — see `images/README.txt` for the exact filenames. Drop matching
files into `/images` and every placeholder box disappears automatically.

**Reviews** (`reviews.html` and the homepage) — the review cards are marked
`[Add a real Google review here]` on purpose. Don't invent testimonials —
copy your actual current Google reviews in, word for word, or embed Google's
own review widget. There's also a "Leave a Review" button that needs your
Google Business Profile Place ID (instructions are in an HTML comment right
above it in `reviews.html`).

**Booking form** (`contact.html`) — the form currently has no backend, so a
submission opens a pre-filled email as a fallback (nothing is ever lost, but
it's not fully automatic). To wire it up properly, pick one:
- **Netlify Forms** (easiest, free): host the site on Netlify, add
  `data-netlify="true"` and a hidden `form-name` input to the `<form>` tag —
  submissions land in your Netlify dashboard automatically.
- **Formspree** or similar: set the form's `action` to your Formspree
  endpoint and set `data-endpoint-ready="true"` on the `<form>` tag.
- Your own backend: same as above, point `action` at your endpoint.

**About page** — the story/history text is intentionally generic. Swap in
your real founding story, certifications, and specifics — that's what
actually builds trust, more than any stock copy can.

**Logo** — the header uses a clean text-based "FL / Fall Line / Auto
Detailing" wordmark, so the site looks finished with zero extra assets. If
you get a real logo file later, replace the `<span class="logo-mark">FL</span>`
+ `<span class="logo-text">…</span>` block (appears identically near the top
of every page) with an `<img src="images/logo.png" alt="Fall Line Auto
Detailing">`.

## 4. Deploying

Any static host works since there's no server-side code:
- **Netlify** — drag the whole folder onto app.netlify.com/drop (also gets
  you free form handling, see above).
- **GitHub Pages / Cloudflare Pages** — push the folder to a repo, enable
  Pages.
- **Traditional hosting (GoDaddy, cPanel, etc.)** — upload the folder via
  FTP/File Manager as-is.

Once you have a domain, update the `<link rel="canonical">` tags and the
`AutoDetailing` JSON-LD block in `index.html` from the placeholder
`falllineautodetailing.com` to your real domain.

## 5. SEO already built in

- Unique `<title>` and meta description per page, targeting the keyword set
  from the brief ("mobile detailing Richmond VA", "ceramic coating
  Richmond", "interior car detailing near me", etc.) naturally in H1s and
  opening paragraphs — not stuffed.
- Each of the 7 city pages has genuinely different copy (not one template
  swapped by name), which is what Google expects from real "service area"
  pages.
- `AutoDetailing` structured data (JSON-LD) on the homepage for local search.
- Fast by default: no JS frameworks, no icon-font/CDN requests, no heavy
  animation — just one CSS file and one small JS file.

## 6. Design notes (why it doesn't look like a template)

The visual system leans on the brand name itself: "Fall Line" is the actual
geological term for where a river drops from higher to lower elevation —
Richmond sits right on the James River's fall line. Instead of the generic
water-droplet/bubble graphics most detailing sites use, the site's background
texture and section dividers use a subtle topographic contour-line motif tied
to that idea, paired with a deep navy + teal palette (`css/style.css`, top
`:root` block — change the `--accent` and `--ink` variables there to retheme
the whole site in one place) and a sticky mobile call/text/book bar that's
genuinely functional, not just decorative.
