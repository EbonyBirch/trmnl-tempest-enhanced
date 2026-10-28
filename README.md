# Tempest Enhanced

An enhanced weather display for **TRMNL OG (including OG V2) and TRMNL X**, powered by the official **Tempest Weather Station** plugin. Shows live conditions and a two-day forecast in full-screen and mashup layouts.

**Latest stable release:** v0.40.0
Based on the fully validated v39 RC14 codebase. Promoted to stable following successful visual inspection and TRMNL stress-testing, with documentation and licensing updates only. No rendering changes.

## Features

- Current temperature, conditions and humidity; today's and tomorrow's minimum/maximum temperatures, UV index and precipitation probability (and amount where supplied).
- Wind gusts and direction; sunrise and sunset.
- Sea-level or station pressure in **hPa**, **mb**, **mmHg** or **inHg**, with a trend arrow.
- Secondary temperature: **Feels Like**, **Wet-Bulb Temperature (WBT)** or **Wet-Bulb Globe Temperature (WBGT)**. Unavailable WBT/WBGT falls back to Feels Like.
- Optional recent lightning activity and/or solar radiation with brightness.
- Independent footer visibility settings for OG and X.
- Localized labels via TRMNL; no fabricated pressure or temperature values when source data is missing.

## Layouts

| Layout | Template | Contents |
| --- | --- | --- |
| Full screen | `full.liquid` | Detailed current conditions and two-day forecast |
| Half horizontal | `half_horizontal.liquid` | Wide current-weather and forecast panels |
| Half vertical | `half_vertical.liquid` | Tall current-weather and forecast panel |
| Quadrant | `quadrant.liquid` | Compact conditions and two-day summary |

All four layouts are available for OG and X. Partial views adapt to mashup slot size and include pressure, wind, sunrise/sunset, the selected secondary temperature and optional readings when available. The quadrant favors a compact day/min/max/UV/precipitation summary; forecast condition descriptions appear on X but are hidden on OG to preserve space. The full-screen X layout also supports portrait orientation.

## Requirements and installation

1. Configure the official **Tempest Weather Station** plugin for your station and keep it active in a playlist or mashup.
2. Install **Tempest Enhanced** from its Recipe page, when available, or import the complete plugin ZIP as a TRMNL Private Plugin.
3. In **Tempest data source**, choose the active native Tempest instance; set your preferred display options.
4. Save, refresh the native Tempest plugin, then refresh Tempest Enhanced.
5. Add its full-screen layout to a playlist or use a partial layout in a mashup.

This is a **Plugin Merge** plugin: it reads the native plugin's data, requires **no separate Tempest API key**, and does not bundle a personal station/instance ID. Available readings depend on the native source. With no usable source temperature, it displays an unavailable-data message instead of `0`.

For manual markup updates, copy **`shared.liquid` and all four layout templates**. TRMNL evaluates Shared before each selected view; the templates are **not self-contained**. Importing an updated ZIP as a separate Private Plugin instance can preserve your existing installation while you test it. Recipe installation behavior should be verified before public release, especially the source-instance selector.

## Settings

| Setting | Choices | Default |
| --- | --- | --- |
| Tempest data source | Active native Tempest instance | Select your instance |
| Pressure Source | Sea level / Station | Sea level |
| Pressure Unit | hPa / mb / mmHg / inHg | hPa |
| Secondary temperature measurement | Feels Like / WBT / WBGT | Feels Like |
| Information below weather icon | None / Lightning / Solar radiation & brightness / Both | None |
| Footer visibility — OG | Show everywhere / Hide everywhere / Hide in all partial layouts / Hide in vertical half / Hide in horizontal half / Hide in quadrant | Show everywhere |
| Footer visibility — X | Same choices as OG | Show everywhere |

The refresh interval configured in `settings.yml` is **30 minutes**. The selected source may have its own update schedule.

### Lightning and solar readings

- **Lightning** displays the last strike's local time and distance plus strike counts for the **last 1 hour / 3 hours**. It requires a complete, positive, non-future last-strike timestamp, a distance and distance unit, both counts, a **positive 3-hour count**, and a strike no older than **3 hours**. `0 / N` is valid when activity occurred only in the preceding three hours. Missing/stale activity hides the row.
- **Solar radiation & brightness** displays **W/m²** and **lux**. A missing individual reading becomes a dash; when both are absent, the row is hidden.
- **Both** displays solar and lightning together in the **partial layouts** and **X full-screen portrait** (when the readings are available). In other full-screen views, **Both** shows only solar/brightness. On OG half-vertical, both fit with the footer shown or hidden.
- When pressure is missing, its value is displayed as `---` alongside the selected pressure unit, rather than inventing a measurement.

### Footer visibility

OG and X have separate controls. **Hide in all partial layouts** means both half layouts and quadrant; full-screen remains visible. Individual hide options affect only the specified layout. Hiding the footer removes its title, icon, instance name and refresh time and frees the reserved height for weather content. The **footer is the only location showing last refresh time**, when available; hiding it does not change the refresh interval.

OG V2 follows the OG setting. If device dimensions are missing or unrecognized, the footer stays visible.

## Localization

Labels use TRMNL's `l_word` filter and `custom_plugins.*` locale entries. Untranslated strings may appear **in English within the corresponding locale files**; this is not a separate plugin-level fallback. Weather descriptions and day overrides come from the native Tempest source.

## Project

**Author:** EbonyBirch · [GitHub repository](https://github.com/EbonyBirch/trmnl-tempest-enhanced) · [Contact](mailto:usetrmnl@aomi.pl)

Further reading: [Development and RC fixes](REVIEW_FIXES.md) · [Validation](VALIDATION.md) · [Publishing and maintenance](PUBLISHING.md).
