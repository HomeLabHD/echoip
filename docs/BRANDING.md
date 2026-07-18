# Branding & theming (HomeLabHD fork)

This image is **stock echoip by default** — set no environment variables and you get the
upstream maintainer's UI unchanged. Branding and theme are opt-in *escape hatches*: they
only take effect when deliberately set. This keeps the image universal and the fork a thin,
rebaseable overlay on upstream.

## Environment variables

| Variable | Effect | Example |
|----------|--------|---------|
| `ECHOIP_BRAND_ICON` | Logo shown in the hero corner. Accepts a URL, a `data:` URI, or a **file path** inside the container (read and inlined as a data URI). Any `png`/`svg`/`jpg`/`webp`/`gif`. | `/opt/echoip/assets/leek.gif` |
| `ECHOIP_BRAND_CAPTION` | Caption text under the logo. | `ipleek.com` |
| `ECHOIP_BRAND_FOOTER` | Footer HTML (replaces the default mpolden/BSD attribution line). | `© 2026 ipleek · Powered by echoip.` |
| `ECHOIP_COLOR_<TOKEN>` | Override one CSS theme token. `<TOKEN>` is the CSS custom-property name upper-cased with `-`→`_`; prefix `DARK_` for the dark theme (so dark vars sort together). | `ECHOIP_COLOR_ACCENT=#2d8b21`, `ECHOIP_COLOR_DARK_ACCENT=#63cf45` |

Color tokens (each also has a `DARK_`-prefixed variant): `BG`, `BG_SURFACE`, `BORDER`, `TEXT`,
`TEXT_SECONDARY`, `ACCENT`, `CODE_BG`, `IP_COLOR`, `HERO_BG`, `CODE_ACCENT`, `JSON_BG`,
`JSON_TEXT`, `JSON_BORDER`, `TABLE_ROW_HOVER`, `TOP_BAR`.

Anything unset falls back to upstream echoip's value, so partial overrides are fine.

## Bundled assets

Brand assets ship inside the image at `/opt/echoip/assets/`, ready to reference by path:

- `leek.gif` — animated leek
- `leek.png` — static leek

## Example: the ipleek.com "leek" theme (Kubernetes)

```yaml
env:
  # branding
  - { name: ECHOIP_BRAND_ICON,    value: /opt/echoip/assets/leek.gif }
  - { name: ECHOIP_BRAND_CAPTION, value: ipleek.com }
  - { name: ECHOIP_BRAND_FOOTER,  value: "© 2026 ipleek · Powered by echoip." }
  # palette — light
  - { name: ECHOIP_COLOR_BG,               value: "#f3f8ee" }
  - { name: ECHOIP_COLOR_BG_SURFACE,       value: "#e8f2e0" }
  - { name: ECHOIP_COLOR_BORDER,           value: "#cde3c0" }
  - { name: ECHOIP_COLOR_TEXT,             value: "#1e3416" }
  - { name: ECHOIP_COLOR_TEXT_SECONDARY,   value: "#52774a" }
  - { name: ECHOIP_COLOR_ACCENT,           value: "#2d8b21" }
  - { name: ECHOIP_COLOR_CODE_BG,          value: "#e8f2e0" }
  - { name: ECHOIP_COLOR_IP_COLOR,         value: "#236a17" }
  - { name: ECHOIP_COLOR_HERO_BG,          value: "#edf6e6" }
  - { name: ECHOIP_COLOR_CODE_ACCENT,      value: "#2d8b21" }
  - { name: ECHOIP_COLOR_JSON_BG,          value: "#1b2d15" }
  - { name: ECHOIP_COLOR_JSON_TEXT,        value: "#e2f3d9" }
  - { name: ECHOIP_COLOR_JSON_BORDER,      value: "#56b03c" }
  - { name: ECHOIP_COLOR_TABLE_ROW_HOVER,  value: "#edf6e6" }
  - { name: ECHOIP_COLOR_TOP_BAR,          value: "#42bc2c" }
  # palette — dark
  - { name: ECHOIP_COLOR_DARK_BG,              value: "#121a0f" }
  - { name: ECHOIP_COLOR_DARK_BG_SURFACE,      value: "#1a2515" }
  - { name: ECHOIP_COLOR_DARK_BORDER,          value: "#334529" }
  - { name: ECHOIP_COLOR_DARK_TEXT,            value: "#e6f3de" }
  - { name: ECHOIP_COLOR_DARK_TEXT_SECONDARY,  value: "#9cbf8d" }
  - { name: ECHOIP_COLOR_DARK_ACCENT,          value: "#63cf45" }
  - { name: ECHOIP_COLOR_DARK_CODE_BG,         value: "#1a2515" }
  - { name: ECHOIP_COLOR_DARK_IP_COLOR,        value: "#86ec6e" }
  - { name: ECHOIP_COLOR_DARK_HERO_BG,         value: "#121a0f" }
  - { name: ECHOIP_COLOR_DARK_CODE_ACCENT,     value: "#63cf45" }
  - { name: ECHOIP_COLOR_DARK_JSON_BG,         value: "#0d1409" }
  - { name: ECHOIP_COLOR_DARK_JSON_TEXT,       value: "#d6ecc9" }
  - { name: ECHOIP_COLOR_DARK_JSON_BORDER,     value: "#63cf45" }
  - { name: ECHOIP_COLOR_DARK_TABLE_ROW_HOVER, value: "#1a2515" }
  - { name: ECHOIP_COLOR_DARK_TOP_BAR,         value: "#63cf45" }
```
