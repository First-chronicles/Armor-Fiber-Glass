# Armor Fiberglass: Website Build Notes

Built October 20, 2026 for Foundational Marketing Hub. A single-page static site with no framework and no build step. It replaces the current IONOS MyWebsite site at armorfiberglass.com. This is a local preview and a ZIP, not a live website.

## Files

- `armor-fiberglass-website.zip`: the `website/` folder, ready to upload. Upload the folder's contents to the web root so `index.html` sits at the top level. Rebuild the ZIP after any edit.
- `website/index.html`: the page, JSON-LD schema and meta tags
- `website/styles.css`: role-based design tokens at the top
- `website/script.js`: menu drawer, dropdowns, forms, lightbox and map. **`FORM_ENDPOINT` is on line 8. The `TOWNS` list for the map is on line 128.**
- `website/assets/img/`: 20 WebP photos (cropped from the 16 supplied photos, white borders removed), plus the logo as PNG and WebP, and a JPG Open Graph image
- `website/assets/favicon-32.png`, `favicon-48.png`, `apple-touch-icon.png`: the logo's shield
- `website/assets/vendor/leaflet/`: Leaflet 1.9.4, hosted locally. It loads only when the map scrolls near the screen.
- `website/robots.txt` (AI crawlers allowed) and `sitemap.xml`
- `Assets/Logo/logo.png`: the logo, downloaded from the current site with approval

## Facts used and their source

All from armorfiberglass.com, read October 20, 2026.

| Fact | Page |
|---|---|
| Phone (661) 323-7373 | Every page |
| Email armorfiberglass@aol.com | Contact/Comments |
| Hours: Monday to Saturday, 7am to 5pm | Contact/Comments |
| California License #897287 | Every page |
| Owner David Paris, "over 29 years" in fiberglass pool resurfacing, on every job, does most of the work himself | About Us, Contact/Comments |
| 5-year warranty and a satisfaction guarantee | About Us |
| Finish lifespan: 10 to 12 years minimum, 15 to 20 years maximum | About Us |
| Resurfaces plaster, concrete, vinyl liner and existing fiberglass | Home, Our Services |
| Fiberglass lowers chemical costs over time and resists stains and algae | Pool Resurfacing & Slides |
| Factory and custom fiberglass and gel-coated slides, "a fraction of the cost" | Pool Resurfacing & Slides |
| New tile, tile matching, tile cleaning and resealing | Our Services, Tile Cleaning |
| Green pool clean-outs, and tub, shower and sink repairs and reglazing | Our Services |
| Free in-home estimates | Tile Cleaning, Our Services |
| "Bakersfield and surrounding areas" | About Us |

## Placeholders to replace before launch

1. **Service-area towns.** On October 20, 2026 the decision was to launch with no extra towns, so the page lists only "Bakersfield" and "Surrounding areas," which matches the client's own wording. If the client later confirms specific towns, add them in five places: the Service Areas dropdown, the service-area checklist, the footer column, `areaServed` in the schema (business and all six Services), and `TOWNS` in `script.js` with each town center's coordinates. The map fits all markers automatically.
2. **Form backend.** Paste a Formspree or GHL URL into `FORM_ENDPOINT` in `script.js`, and replace `REPLACE_FORM_ID` in the two form `action` attributes in `index.html` (the no-JavaScript fallback). With the endpoint empty, the forms run in demo mode: the thank-you message says nothing was sent. Real success shows only on an OK response from the backend.
3. **Production domain.** The canonical tag, Open Graph tags, schema and sitemap all use `https://www.armorfiberglass.com/`. The host needs an SSL certificate before launch.
4. **Social links.** None were found on the current site, so there are no social icons and no `sameAs`. A comment in the footer marks the spot. Add the Google Business Profile and Facebook URLs once confirmed.
5. **Blog.** The three cards are labeled "Coming soon" and do not link anywhere. Replace them with real posts on their own pages.
6. **Slide photo.** The "Slides, Tubs & Showers" card uses a brushed-steel panel with an icon because no slide, tub or shower photo was supplied. Swap in a real job photo when the client has one.

## Decisions made with defaults, so confirm with the client

- **Address is treated as private.** The only address on the current site is PO Box 5592, Bakersfield, CA 93388. The page shows "Bakersfield, CA" only, the schema has city, state and country but no street, and the map plots Bakersfield's city center. If the client has a public, staffed address that matches the Google Business Profile, add it.
- **"Over 29 years."** The About page may be several years old, so the real number may now be higher. The page says "more than 29 years," which stays true either way. Update it if the client gives a current figure.
- **Before & after pairs were matched by eye** (same fences, diving boards, planters and tile). The current site shows its photos in before/after pairs but does not say which are which job. Confirm the six pairs: green pool (photos 3 and 4), peeling plaster (7 and 8), kidney pool (12 and 13), stained pool (14 and 15), hot tub (10 and 11), spa (1 and 2). Photos 5, 9 and 16 are used only as the repair card and the CTA background, or not at all.
- **Left off on purpose:** the current homepage's "Southern California's leading fiberglass pool refinishing experts." Nothing supports that superlative.
- **Schema type is `HomeAndConstructionBusiness`.** Schema.org has no pool-resurfacing type. The license is in `hasCredential`, and David is listed as `employee` with the job title Owner.
- **Palette.** The logo is monochrome chrome, so the steel and gunmetal tones come from it. The pool-tile blue and aqua come from the job photos, and amber is the call-to-action color for contrast. All text pairs meet WCAG AA.
- **No reviews or ratings** anywhere on the page or in the schema, because none were supplied.

## Verification done (October 20, 2026, over local HTTP)

- Exactly one H1 ("Fiberglass Pool Resurfacing in Bakersfield, CA"), and a clean H2/H3 outline
- Title is 58 characters and the meta description is 153 characters
- The JSON-LD parses: the business, 6 Services, WebSite, and an FAQPage with 7 questions that match the visible FAQ
- No horizontal overflow at 320, 375, 768, 1024 or 1366px. The side gutter is 16px on mobile.
- No broken images and no console errors. Every image has width and height, the hero is preloaded with `fetchpriority="high"`, and everything below it is lazy-loaded.
- All in-page anchors resolve
- The desktop caret dropdowns open, and the mobile drawer shows the services and towns as indented items. Escape closes both.
- Form validation works (missing name or phone, bad email). The demo-mode thank-you message appears, and the "Ask About..." buttons preselect the service in the contact form.
- The lightbox opens and steps through all 12 before/after photos
- The map loads with a Bakersfield marker and Esri attribution

## Not verified

- Core Web Vitals. The page is light (the largest image is 36 KB), but run PageSpeed Insights once it is live on HTTPS.
- Google Rich Results Test. Run it on the live URL.
- The CSLB license status for #897287 was not checked. Look it up at cslb.ca.gov before launch.

## Photo quality

The supplied photos are small (about 450 to 520px wide). Cards and before/after pairs look fine. The hero and the two photo bands are upscaled under a dark overlay with a slight blur so the softness doesn't show. Larger originals from the client's phone would make a visible difference.

## Client actions

- Confirm the towns, the before/after pairs and the current years of experience.
- Claim and verify the Google Business Profile, and complete it: the right primary category (for example Pool Cleaning Service or Swimming Pool Repair Service), hours, services, and 10 or more real job photos. Keep the name, phone and city identical to the site.
- Ask customers for reviews steadily and reply to each one. Add review schema only once there are genuine reviews to show.
- List the business in local and trade directories with the same name, phone and city.
- Add armorfiberglass.com to Search Console and submit the sitemap after launch.
