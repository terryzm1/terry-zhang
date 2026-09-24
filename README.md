# 张天予 · Tianyu (Terry) Zhang — Personal Site

A one-page personal site built with vanilla HTML and CSS.

## Live Site

zhang-tianyu.com

## The design

Ivory ground, one matcha accent, and the name as the mark. Type is
[Instrument Sans](https://fonts.google.com/specimen/Instrument+Sans) for everything, with
[Noto Serif SC](https://fonts.google.com/specimen/Noto+Serif+SC) for the Chinese display glyphs.

- **Landing** — 张天予 alone on a full screen, drawn in once per page load. The first scroll
  hands off to the bio and removes the landing from the document, so the top of the page is the
  bio from then on.
- **Bio** — running paragraphs with the key phrases underlined or washed in matcha, beside the
  portrait.
- **Projects** — cards linking to [github.com/terryzm1](https://github.com/terryzm1). No files are
  served from this site.
- **Interests** — a grid of mixed-size photo slots.
- **Contact** — a matcha panel with a mailto link.

## Interaction

All of it lives in one inline `<script>` at the bottom of `index.html`.

| | |
|---|---|
| Landing hand-off | First scroll, click or key pins the scroll at 0, fades the name out, removes it, then fades the page in. The scroll stays pinned for ~2.3s so momentum cannot overshoot the bio. |
| Chrome | The nav pills stay hidden until the reader scrolls or clicks. |
| Nav | Sliding highlight, scroll-spy, and the current section shown in bold. |

Everything degrades: `prefers-reduced-motion` turns the hand-off into a cut, and the section
fades are behind `@supports (animation-timeline: view())`.

## Theme

Every colour is a custom property on `:root`, so a theme is just a different set of values.

- By default the site follows the operating system, via `prefers-color-scheme: dark`.
- The toggle in the nav writes `light` or `dark` to `data-theme` on `<html>` and remembers the
  choice in `localStorage`, which overrides the system setting.
- A small script in `<head>` applies the stored choice before first paint, so a reader who picked
  dark never sees a white flash.

The dark values appear under two selectors — `:root:not([data-theme="light"])` inside the media
query, and `:root[data-theme="dark"]` outside it — so the system default still works without
JavaScript.

## Adding photos

Each card declares its own grid span, so a photo can change size without moving the rest of the
grid. To fill a slot, replace the `<div class="ph">…</div>` placeholder with:

```html
<div class="card-media"><img src="your-photo.webp" alt="Description" loading="lazy"></div>
```

Slots waiting on images: photography (3:4), travel (16:9), flute (1:1), volleyball (1:1).

## A note on the CJK font

`Noto Serif SC` is loaded subset to the characters used as display marks (`张天予作码`) via the
`&text=` parameter — a couple of KB rather than a full CJK face. Any new Chinese character used at
display size must be added to that list in `index.html` or it falls back to a system serif.

## Getting Started

```bash
python3 -m http.server 4173
```

Then open http://localhost:4173. No build tools or dependencies.

## Project Structure

```
terry-zhang/
├── index.html         # Page and its inline script
├── styles.css         # Stylesheet
├── portrait.webp      # Portrait
├── resumepg.pdf       # Resume (PDF)
├── LICENSE            # MIT License
└── README.md          # This file
```

## License

[MIT](LICENSE).

## Contact

- **Email:** terryzhang001@icloud.com
- **GitHub:** [github.com/terryzm1](https://github.com/terryzm1)
- **LinkedIn:** [linkedin.com/in/terryzm](https://linkedin.com/in/terryzm)
