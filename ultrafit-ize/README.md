# ULTRAFIT North

A static rebuild of `ultrafitalex.com` (ULTRAFIT West Coast / Alex Dinh), rebranded to
**ULTRAFIT North / Ize**. Layout, CSS, JS and DOM structure are identical to the source —
verified by diffing the rendered DOM skeleton: the only structural difference is one
removed `<script type="speculationrules">` block.

## Run it locally

```bash
cd /Users/pham/Documents/ultrafit-north && python3 -m http.server 8791
```

Then open http://localhost:8791.

Serve from the **site root**. Elementor's lazy-loaded JS chunks are resolved from
root-relative paths (`/wp-content/plugins/...`), so a subdirectory deploy will break the
hero video and the nav/form handlers.

## What changed from the source

| Source | This site |
| --- | --- |
| ULTRAFIT West Coast | ULTRAFIT North |
| "Direct Access to ULTRAFIT on the West Coast" | "Direct Access to ULTRAFIT in the North" |
| Alex Dinh / ALEX DINH | Ize / IZE |
| `ultrafitalex.com` | `ultrafitize.com` |
| `alex@ultrafitwestusa.com` | `ize@ultrafitnorthusa.com` |
| `510-493-6185` | `763-722-0092` |
| `instagram.com/ultrafit.alex` | `instagram.com/ultrafit_protection_usa` |
| © 2026 ULTRAFIT Alex | © 2026 ULTRAFIT North |
| Territory map: 11 western states | Midwest + Northeast (see below) |
| State dropdown: CA, NV, AZ, OR… | 27 northern states + DC |

Also removed: WordPress feed / oEmbed / REST / shortlink `<link>` tags and the generator
meta, all of which pointed at the old site and would 404.

## Headshot

The "Meet Ize" slot shows a **Coming Soon** card
(`wp-content/uploads/2026/05/Meet-Ize-coming-soon.svg`) — a 791×699 SVG built from the
site's own palette (`#165DA3` accent, `#6EC1E4` glyph, Inter).

Alex Dinh's photo has been deleted from the tree entirely, along with its `-300x265` and
`-768x679` variants. The social-preview `og:image` and the JSON-LD `primaryImage`, which
both pointed at that photo, now point at `ultrafit-usa-logo.svg`.

To drop in a real photo later: save it as `Meet-Ize.webp` at 791×699 and change the
`<img src>` back — the `<img>` still carries `width="791" height="699"`, so the layout
won't shift.

## Territory

Taken from the ULTRAFIT installer map (`ultrafit-installer-map-1024x676.png`), where the
North region is the green block:

> ND, SD, NE, KS, MN, IA, MO, WI, IL, MI, IN, OH, KY, WV, VA, PA, NY, NJ, DE, MD, DC, CT,
> RI, MA, NH, VT, ME

- **Map** — `Territory-North.webp` (+ `-768x507` / `-300x198` variants). Generated from the
  installer map with the orange (West) and blue (South/Texas) regions greyed out; the green
  North region is untouched.

  The greyed states use `#252525`, not a light grey — that's what the source site's own
  territory map used, because this section sits on a near-black `#171717` background and a
  light grey would glow instead of recede. State borders and labels inside the greyed
  regions were remapped to `#3e3e3e` / `#5c5c5c` so they stay faintly legible.

  The installer map's aspect ratio (1.515) differs slightly from the old territory image's
  (1.554), so the `<img>` height attribute went from 515 to 528. Rendered width is
  unchanged at 800px.

- **State dropdown** — now lists those 27 states plus DC, Minnesota first (matching the
  763 area code), then alphabetical, then "Other".

## ⚠️ The two forms do not submit

Both are Elementor Pro AJAX forms. They post to
`https://ultrafitize.com/wp-admin/admin-ajax.php`, which only exists if this runs on a
WordPress install with Elementor Pro. On static hosting the markup renders but submissions
go nowhere — either deploy into WordPress, or repoint the forms at a form service
(Formspree, Netlify Forms, etc.).

## Other notes

- The hero background is a **YouTube** background video, `uFqb7K9GJH8` — the same clip the
  source site uses. It's ULTRAFIT booth footage, not Alex-specific, so it was kept.
  Swap the ID in the hero container's `data-settings` to change it.
- Fonts (Roboto, Roboto Slab, Inter) still load from Google Fonts — internet required.
- **Tidio live chat** is loaded from a `<script>` just before `</body>`. The supplied
  snippet used a protocol-relative `//code.tidio.co/…`; it's written as explicit
  `https://` so it also works when testing over plain http.
- Photography other than the headshot is generic ULTRAFIT/stock product imagery and was
  carried over as-is.
- **Fixed a bug inherited from the source site.** Its "Text" button linked to
  `http://sms+15104936185` — malformed, so it did nothing. That's now `sms:+17637220092`.
  Its "Email" buttons also used `mailto:%20alex@…`, with an encoded leading space that some
  clients reject; those are now plain `mailto:ize@ultrafitnorthusa.com`. Revert both if you want
  a byte-exact clone of the original behaviour.
