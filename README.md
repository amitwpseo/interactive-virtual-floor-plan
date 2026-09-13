# Interactive Venue Map

A Claude skill + example output for turning a static venue floor plan (image or PDF) into a **pixel-accurate, interactive HTML/SVG floor plan** — pan, zoom, search, category filters, and a click-to-view info drawer for every booth, stage, and attraction. Built for dropping into WordPress/Elementor as a custom HTML block, or any site that accepts raw HTML.

## What's in this repo

| File | What it is |
|---|---|
| `interactive-venue-map.skill` | A [Claude skill](https://www.anthropic.com/news/skills) — install it in Claude to have it build one of these maps for you from a reference image |
| `example-floorplan.html` | A working, self-contained example output — open it in a browser or paste it into an HTML block to see the pattern live |

## Using the skill

1. Save `interactive-venue-map.skill` into your Claude skills (via the "Save skill" option when the file is shared in a Claude conversation, or your org's skill catalog).
2. Upload a reference floor plan (image or PDF) to Claude and ask for an interactive version — e.g. *"turn this venue map into a clickable floor plan for my site."*
3. Claude will trace the reference image at 1:1 coordinates (grid module size, columns, zones), then generate a single self-contained HTML file with:
   - Pan & zoom (mouse drag, scroll wheel, touch pinch)
   - Live search across booth name/ID/type
   - Category filter pills (stages/attractions, VIP, reserved, available)
   - A slide-in info drawer per booth
   - A "view static map" lightbox fallback showing your original reference image

If you already have a map built this way and something's missing or mis-sized, ask Claude to re-check it — the skill instructs it to go back to the **original reference image**, not the previous HTML draft, since that's the actual source of truth.

## Using the example file

`example-floorplan.html` is fully generic — no real event branding, links, or logos — so it's safe to use as a starting template. To adapt it to your own event:

1. **Swap the logo** — replace the dashed placeholder box (`id="zone-event-logo"`) with your own `<image href="...">` logo asset.
2. **Update booth data** — each clickable space is an SVG `<rect class="vfp-item">` with `data-id`, `data-name`, `data-type`, `data-status`, and optional `data-desc` attributes. Edit these to match your real floor plan.
3. **Set your app / info link** — the drawer's call-to-action button currently points to `#`; point it at your event app or info page.
4. **Add your static map image** — the "View Static Map" lightbox has an empty `src` on its `<img>`; point it at your high-res reference blueprint.
5. **Adjust the color legend** — red/blue/white map to reserved/VIP/available by default; change the fills and the `.leg-*` classes in the footer legend to match your own scheme.

## Notes

- Everything is a single self-contained HTML file — inline CSS and JS, only Google Fonts and Font Awesome loaded from CDN. No build step.
- Mobile breakpoints are included (stacked controls, full-height drawer, scrollable filter pills).
- This is presentational/interactive only — it doesn't include a booking or CMS backend. Booth "reserved/available" status is set per-element via `data-status` and the `booth-avail` class.

## License

Use and adapt freely for your own events.
