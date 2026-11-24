# Shambhavi Kulkarni — Fine Art

A single-page portfolio site for a Bengaluru-based painter, published with GitHub Pages.

## Structure

```
index.html          # the entire site — markup, styles and behaviour in one file
404.html            # Pages not-found page
assets/             # web-optimised artwork (JPEG, max 1400px, stripped metadata)
  hero-painting.jpg
  golden-dusk.jpg
  still-waters.jpg
  sacred-ground.jpg
  first-bloom.jpg
  midnight-reverie.jpg
  og-image.jpg      # 1200×630 social share card
.github/workflows/static.yml   # deploys the repo root to GitHub Pages on push to main
```

No build step, no dependencies. Edit `index.html` and push to `main`; the workflow deploys it.

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Editing content

- **Artwork** — each piece is a `<figure class="work">` in the gallery section. It carries
  `data-src`, `data-title`, `data-meta`, `data-status`, `data-desc` and `data-cat`
  (`landscape` | `botanical` | `abstract`). The lightbox, filter counts and captions all read
  from these attributes, so adding a work is a copy-paste of one block plus a new image in `assets/`.
- **Colour and type** — all tokens live in `:root` at the top of the stylesheet.
  `--gold` is decorative only; use `--gold-deep` for small text so it stays above 4.5:1 contrast
  on both the cream and parchment grounds.
- **Contact address** — set `STUDIO_EMAIL` near the top of the `<script>` block, and update the
  `mailto:` links in the mobile menu, form and footer.

## Enquiry form

The form validates on the client, then opens the visitor's email app with every answer
pre-filled, addressed to `STUDIO_EMAIL`. Nothing is sent to a server and no data is stored.

To collect enquiries without relying on the visitor's mail client, point the `<form>` at a
service such as Formspree and remove the `mailto:` handoff in the submit handler.

## Before going live

- [ ] Replace `studio@shambhavikulkarni.art` with the real address.
- [ ] Replace the placeholder social links in the footer (Instagram, Pinterest, Behance).
- [ ] Update the canonical URL, `og:url`, `og:image` and `twitter:image` if the site moves
      from `adithyakulkarni93-prog.github.io/DCET-2026/`.
- [ ] Confirm the works, prices and availability shown in the gallery are accurate.

## Accessibility & performance notes

- Semantic landmarks, skip link, visible focus rings, labelled form controls and error messages
  wired with `aria-describedby`/`aria-invalid`.
- Gallery filter uses `aria-pressed` and announces the result count via `aria-live`.
- The lightbox is a native `<dialog>` with keyboard (← →, Esc) and swipe support.
- All motion is disabled under `prefers-reduced-motion: reduce`; the custom cursor only
  appears on fine-pointer devices.
- Images are lazy-loaded except the hero, which is preloaded; every image has intrinsic
  `width`/`height` so the layout does not shift while loading.
