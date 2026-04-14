# @koehler8/cms-theme-frog — Lush Canopy

- **Slug**: `frog`
- **Version**: 1.0.0
- **Author**: koehler8

## Install

```bash
npm install @koehler8/cms-theme-frog
```

```js
// vite.config.js
import cms from '@koehler8/cms/vite';

export default {
  plugins: cms({ siteDir: './site', themes: ['@koehler8/cms-theme-frog'] }),
};
```

Set `site.theme` to `"frog"` in your site config. If external font calls are restricted, host the Google Fonts locally and adjust the `@import` in `theme.css`.

## Visual Direction
- Deep forest palette with emerald gradients, misty overlays, and soft glass borders.
- Card/layout chrome leans heavily on green glows; headline/status ribbons reuse the same tints for cohesive KPI sections.
- CTA/buttons use a lush ignition gradient; hero/backdrop layers add atmospheric radials suited for dark photography.

## Token Highlights
- Rich helper/tab/field surfaces tuned for dark canvases; chip/outline treatments rely on the mint accent family.
- Countdown/status/chart tokens are explicitly defined so presale widgets stay legible on the dark base.
- Generous radii (up to 28px) and high-contrast helper rails pair with the theme’s raised shadows.

## Compatibility Notes
- Works best with dark hero art or illustration; avoid pairing with stark white imagery unless you add per-section overlays.
- Theme CSS customizes legacy components (status metrics, stake buttons, About block) via `[data-site-theme="frog"]` selectors—keep bespoke overrides in this folder to avoid cross-site bleed.
