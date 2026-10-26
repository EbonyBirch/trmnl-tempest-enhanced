# Tempest Enhanced

Version **39 RC5** — all four layouts for TRMNL OG and X.

An enhanced weather display for TRMNL OG and TRMNL X, using live readings and forecasts from the official **Tempest Weather Station** plugin.

## Supported layouts

All four standard TRMNL layouts are supported:

| Layout | File | Display |
| --- | --- | --- |
| Full screen | `full.liquid` | Detailed current weather and two-day forecast |
| Half horizontal | `half_horizontal.liquid` | Wide current-weather and forecast panels for stacked mashups |
| Half vertical | `half_vertical.liquid` | Tall current-weather and forecast panel for side-by-side mashups |
| Quadrant | `quadrant.liquid` | Compact current readings and two-day forecast summary |

Partial layouts adapt the presentation to the available space. The quadrant summarizes forecasts with day, minimum/maximum temperature, UV and precipitation rather than forecast condition descriptions. All layouts retain pressure, humidity, wind gusts and direction, sunrise/sunset, the selected secondary temperature, and the optional lightning or solar information.

## Features

- Current temperature, weather conditions and humidity.
- Today's and tomorrow's forecasts, including minimum/maximum temperature, UV index and precipitation probability; precipitation amount appears when supplied.
- Wind gusts and direction, sunrise and sunset.
- Sea-level or station pressure, selectable in **hPa**, **mb**, **mmHg** or **inHg**, with a pressure-trend indicator.
- Secondary temperature selection: **Feels Like**, **Wet-Bulb Temperature (WBT)** or **Wet-Bulb Globe Temperature (WBGT)**. If the selected wet-bulb measurement is unavailable, Feels Like is used.
- Optional **recent lightning activity**, **solar radiation and current brightness**, or **both on partial layouts and X full-screen portrait**. Select **None** to leave this information hidden.
- Localized labels through TRMNL's `l_word` filter and `custom_plugins.*` locale entries.
- Separate footer visibility controls for **OG** and **X**, with the footer shown everywhere by default. The footer is the only place that displays the last refresh time, when available.
- A no-data message when no usable source temperature is available, instead of a misleading zero reading.

## Requirements

- An existing official Tempest Weather Station plugin configured for your station.
- That native plugin active in a playlist or mashup so it can be selected as the data source.
- TRMNL Plugin Merge support and the enriched Tempest readings supplied by the native plugin/backend.

This plugin reuses the native plugin's data. It does not require a separate Tempest API token and does not contain an account-specific source instance ID. Availability of individual readings depends on the source data.

## Installation

1. In TRMNL's **Private Plugin** settings, choose **Import new** and import the ZIP.
2. Open the imported plugin's settings.
3. Under **Tempest data source**, select your active native Tempest Weather Station instance.
4. Choose pressure source and units, secondary temperature, optional weather information, and footer visibility for OG and X.
5. Save and refresh the native Tempest plugin, then refresh the enhanced plugin.
6. Use the full-screen layout in a playlist or choose the appropriate partial layout in a mashup.

When upgrading, importing as a new private plugin lets you retain your existing installation until you have selected the data source and copied your preferred settings.

## Configuration

| Setting | Choices | Default |
| --- | --- | --- |
| Tempest data source | Active native Tempest instance | Select your instance |
| Pressure Source | Sea level / Station | Sea level |
| Pressure Unit | hPa / mb / mmHg / inHg | hPa |
| Secondary temperature measurement | Feels Like / WBT / WBGT | Feels Like |
| Information below weather icon | None / Lightning / Solar radiation & brightness / Both (partial layouts and X full-screen portrait; see below) | None |
| Footer visibility — OG | Show everywhere / Hide everywhere / Hide in all partial layouts / Hide in vertical half only / Hide in horizontal half only / Hide in quadrant only | Show everywhere |
| Footer visibility — X | Same layout choices as OG | Show everywhere |

In partial layouts, optional information appears in a compact row near the current readings. Temperature and other source-provided units follow the native Tempest data; pressure units are configured here.

## Lightning and solar information

Lightning appears when Lightning mode is selected, or in Both mode on eligible partial layouts or X full-screen portrait, and the timestamp, distance, distance unit, and both rolling strike counts are available. The last strike must have a positive, non-future timestamp, be no more than three hours old, and the three-hour count must be greater than zero.

The summary displays local last-strike time, distance and the **last 1 hour / last 3 hours** strike counts. A `0 / N` count remains visible when activity occurred within three hours but not within the last hour. Missing, stale or zero-activity data leaves the row empty. Local strike time uses the source's UTC offset.

Solar mode displays radiation in **W/m²** and brightness in **lux**. If only one reading is available, the missing value is shown as a dash; if both are missing, the row is hidden.

Missing pressure is shown as `---` followed by the selected unit. No synthetic pressure reading is substituted.

## Localization

Labels use the corresponding TRMNL locale files. Strings that have not yet been translated are already present **in English within the corresponding locale files**. There is no separate plugin-level localization fallback. Weather condition descriptions and day overrides are supplied by the native Tempest plugin.

## Author and contact

- Author: **EbonyBirch**
- Source code and project page: [EbonyBirch/trmnl-tempest-enhanced](https://github.com/EbonyBirch/trmnl-tempest-enhanced)
- Contact: [usetrmnl@aomi.pl](mailto:usetrmnl@aomi.pl)

Public author and contact details are configured in the `author_bio` entry in `settings.yml`.

## Package

The import ZIP contains `settings.yml`, `full.liquid`, `half_horizontal.liquid`, `half_vertical.liquid`, `quadrant.liquid`, and this README at its root. Each layout is self-contained; no shared Liquid file is required.

Version 39 RC5 retains the accepted v38 landscape and partial layouts and adds the approved X full-screen portrait arrangement: a large weather icon over the current temperature and aligned measurements. Wide current temperatures use smaller native font tiers. The portrait layout supports combined solar/brightness and recent lightning. All readings use live source data; no mock values or forced setting overrides are included. X portrait layouts were accepted after visual testing through test13.

## Footer visibility

**Footer visibility — OG** and **Footer visibility — X** independently control the title bar on the two device families. Both default to **Show everywhere**, preserving the standard appearance when no choice has been made.

Each dropdown offers: Show everywhere, Hide everywhere, Hide in all partial layouts, Hide in vertical half only, Hide in horizontal half only, and Hide in quadrant only. “All partial layouts” means both half layouts and the quadrant; full screen keeps its footer.

**The footer is the only place on the display that shows the last refresh time, when available.** Keep it enabled for any layout where you want that timestamp visible. Hiding it does not move the timestamp elsewhere or change the refresh interval.

Hiding the footer removes its icon, title, instance name and refresh time, and releases the reserved height for weather content. These settings belong to the plugin instance and apply wherever that instance is used. OG also covers OG V2; X uses the TRMNL X device class. Other device classes keep the footer visible.

### Combined solar/brightness and lightning

Select **Both solar/brightness and lightning (partial layouts + X portrait, check README.md)** to show both readings. Lightning still appears only when recent lightning data is available. X full-screen portrait displays solar/brightness followed by recent lightning beneath pressure. Other full-screen views show solar/brightness only when Both is selected.

On **OG vertical-half**, both readings fit only with the footer hidden. With the footer visible, Both automatically displays **solar radiation/brightness only**. To see both, set **Footer visibility — OG** to **Hide in vertical half only**, **Hide in all partial layouts**, or **Hide everywhere**. The plugin respects your footer choice; it does not hide the footer automatically. Remember that the footer is the only place showing the last refresh time. This restriction does not apply to X.

## Release candidate validation

This is a private release candidate for testing, not a published Recipe. Import as a new instance, select your native Tempest source, and refresh. Verify all settings with live data, including no recent lightning, each optional-information mode, pressure units, secondary-temperature selection, and footer policies. Check the final live-data renders before capturing submission screenshots. Before public submission, configure the Recipe icon and featured image in TRMNL, run Chef, resolve its findings with the TRMNL team, and ensure the public repository contains the matching source, README, licence and attribution.

## RC4 accepted portrait layouts

X portrait layouts were visually reviewed by the author through test13. Full view includes a condition caption below the main icon. Half-horizontal uses main/supplementary above today/tomorrow, with continuous separators. Half-vertical stacks lightning below solar information. Quarter allows the current condition caption to wrap.

This package uses live native Tempest data only; settings remain user-controlled. The separate Summer Demo package is synthetic and must not replace the live recipe. The supplied icon is included at `assets/plugin-icon.png`; upload/select it in TRMNL recipe settings.

## RC4 layout updates

Incorporates Summer Test 4 layout adjustments: X full-screen main temperatures use 220/170/128 px for 1/2/3+ characters including minus; updated current weather icon sizes and vertical position; X landscape half-horizontal lightning aligns with sunset; portrait half-horizontal description increased one font step. All weather readings and user selections come from the native live source. No demo fixture or forced demo settings.

## Final RC4 adjustment

OG quarter current weather icon reduced a further 6% (109.44 to 102.8736 CSS px). Other layouts retain the accepted RC3 behaviour. Live readings and user-selected options remain unchanged.

## RC5 release notes

- Default plugin name: **Tempest Enhanced**; the RC version is tracked in this README and archive filename.
- OG full-screen main weather icon retains the accepted 20% reduction (22cqw to 17.6cqw).
- Optional information defaults to **None**. The experimental full-screen Both change is not included: full-screen OG and X landscape show only solar/brightness for Both; X portrait retains combined readings.
- All temperatures, conditions, timestamps and optional readings use the selected native Tempest source. No summer fixture, frozen clock or forced demo selections are included.
- Expanded About This Plugin description for the public Recipe page, including setup instructions and source dependency.

## Public Recipe description

Tempest Enhanced brings detailed readings from your Tempest weather station to TRMNL OG and X, with full-screen and mashup layouts for a quick view of current conditions and the next two days. See temperature, humidity, wind gusts and direction, sunrise and sunset, forecast highs and lows, UV index, and precipitation information. Choose sea-level or station pressure in four units, with a trend indicator, and switch the secondary temperature between feels-like, wet-bulb temperature, and wet-bulb globe temperature when available.

Optional readings add solar radiation, brightness, or recent lightning activity with the last strike time, distance, and one-hour and three-hour counts. Combined readings depend on the layout; see the README for details. Separate footer controls let you adjust OG and X independently.

To get started, configure the official Tempest Weather Station plugin and keep it active in a playlist or mashup. Select that instance under Tempest data source, save, and refresh both plugins. No separate Tempest API token is required. Readings depend on the native source, and lightning is hidden when activity is stale or unavailable.

Created by EbonyBirch, using TRMNL's native Tempest data and localization. Find setup instructions, source code, and issue reporting in the linked GitHub project.

## Publishing checklist

1. Import this live RC as a new private plugin, select your active native Tempest source, and refresh both plugins. Verify the final live screens and settings; keep the mock separate.
2. Update the linked public GitHub repository with this version's source and README, the appropriate licence and retained upstream attribution. Include representative screenshots under screenshots/ and link them from the README. Mark any summer screenshot as simulated data.
3. In TRMNL settings, check the name, About This Plugin description, author/contact links and categories. Upload/select assets/plugin-icon.png. Choose a representative rendered screen for the featured image using the Recipe preview-image control where available.
4. Click Publish plugin? and follow the public submission flow. Review Chef's findings and resolve them before submitting, or discuss necessary layout exceptions with TRMNL. Local syntax validation is not a Chef approval.
5. Submit for manual TRMNL review. If requested, supply the separate summer demo to demonstrate lightning without waiting for a storm; publish the live version, not the hardcoded mock.
6. After publication, test future changes in a clone before updating the Recipe Master, because installed Recipes receive its updates.

Reference documentation:
- https://help.trmnl.com/en/articles/10122094-plugin-recipes
- https://help.trmnl.com/en/articles/11395668-recipe-best-practices
- https://help.trmnl.com/en/articles/12772238-demo-data-for-publishing-plugins

The author_bio description exceeds TRMNL's 100-word threshold for external search-engine visibility. This threshold does not change TRMNL's own search. Publication and Chef review have not been performed for this archive.
