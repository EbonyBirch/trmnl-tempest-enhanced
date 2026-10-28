# Development history and review fixes

This document records the releases, technical fixes, and review findings that led to **Tempest Enhanced v0.40.0**. Entries are listed **newest first**.

Older release-candidate notes are preserved for historical reference. Their instructions to rerun checks, warnings about incomplete validation, and descriptions of previous behavior reflect the state of those particular builds—not outstanding requirements or the behavior of the stable release. For current features and installation instructions, see [README.md](README.md).

## v0.40.0 — Initial stable release (2026-10-28)

**Source baseline:** v39 RC14 (unchanged rendering and configuration).

The validated **v39 RC14** codebase was promoted to **v0.40.0** after successful visual inspection and TRMNL stress-testing. This is a **stable-release designation and documentation update, not a new rendering build**.

Changes accompanying the release:

- Simplified and reorganized `README.md` to focus on current features and usage.
- Consolidated historical development notes in this file and reordered the release-candidate entries newest first.
- Updated documentation to reflect completed validation rather than pending RC tests.
- Added CC BY 4.0 licensing and attribution information.

**No Liquid template, rendering-logic, `settings.yml`, or layout changes were made.** The plugin's functional baseline remains **v39 RC14**.

## Historical release candidates (newest first)

### RC14 — Live-data baseline (TEST14–TEST16)

Includes the layout refinements from TEST14–TEST16, with no synthetic readings:

- X landscape quadrant: both primary metric blocks have the same width and left edge, preserving their location in the right half regardless of label length.
- X portrait half-horizontal: removed tomorrow's extra 18px left padding; both forecast temperature pairs align to the right above their icons.
- Removed the central lightning test override and all mock footer labels. Lightning requires complete, recent, real source data again.
- Retained restored portrait full-screen separators, compact lightning counts where needed and OG half-vertical **Both** support with either footer state.
- Default plugin name is **Tempest Enhanced**; saved custom instance names are preserved.

### RC13 — Intermediate test builds

The source archive contains no standalone RC13 release notes. RC14 validation references the live RC13 data-calculation baseline; TEST14–TEST16 were subsequently incorporated into RC14. No undocumented change list is inferred here.

### RC12 — Visual refinements

- X landscape quarter: reduced feels-like/humidity values one native step (base to small), placed them in a vertical stack on the right of the current conditions, feels-like first. X portrait retains its previous value size and layout.
- OG quarter: reserved 96px minimum header height and adjusted row allocation so the current caption, auxiliary readings and forecast no longer compete for the same vertical space.
- OG half-vertical: reduced section gaps from 6px to 4px, metric padding/row gaps to 4px, forecast vertical padding from 6px to 4px and forecast inner gaps from 4px to 3px. Forecast rows now follow content height instead of distributing spare space between the days.
- Full and half-horizontal layouts, Shared and settings are unchanged from RC11.

Spacing changes are layout refinements; native text-size classes remain in use. Hosted visual confirmation is still required.

### RC11 — Small compatibility fix

Removed the unsupported `lg:mt--small` class from the full-screen wind/pressure row. No replacement margin was added, preserving the existing spacing. All other plugin code and settings are unchanged from RC10.

### RC10 — Review fixes

- X portrait half-vertical: both forecast temperature pairs now use `lg:value--small`; removed the larger portrait override.
- X quadrant: UV/precipitation details use `lg:label--base` and forecast descriptions use `hidden lg:visible`. Forecast temperatures remain `lg:value--small` to avoid colliding with the neighboring day. OG descriptions remain hidden.
- Partial measurements and sunrise/sunset use native two-column grids; forecast temperatures use `text--right`; forecast day separators use native dividers. Existing special positioning, gaps and device-specific geometry remain scoped.
- Full screen: removed all custom font-size rules. Native classes now directly select the established X main-temperature sizes: 1 character `giga`, 2 characters `mega`, 3+ characters `xxxlarge`. The minus sign counts; the degree symbol does not. Portrait measurement labels use the native base label size.
- Full-screen portrait column counts use native responsive grid classes.

The default public name is **Tempest Enhanced**, with no RC suffix. The footer displays the saved instance name. If an existing instance or Recipe Master is named “Tempest Enhanced RC9”, rename it to **Tempest Enhanced** in TRMNL settings; importing code does not necessarily replace a saved name. Personal instance names remain supported.

References: [visibility](https://trmnl.com/framework/docs/3.3/visibility), [grid](https://trmnl.com/framework/docs/3.4/grid), [divider](https://trmnl.com/framework/docs/3.4/divider).

### RC9 — Review fixes

- Removed the full view's redundant framework wrappers in both data and missing-data branches.
- Added `shared.liquid` for translations, source handling, measurements, conversions and temperature-size selection. TRMNL runs Shared before the selected view; no include/render tag is needed.
- Footer visibility now conditionally omits `title_bar`, retaining independent OG/X preferences. Removed footer-hiding CSS and reserved-height overrides. Device dimensions identify OG (800 × 480) and X (1872 × 1404), in either orientation.
- Replaced simple portrait visibility/direction rules with native responsive utilities, removed 72 redundant CSS declarations, and removed all inline style attributes from the four views. Precise custom geometry and temperature sizing remain where needed to preserve the accepted layouts.
- Shortened the lightning option and removed the README reference from Both. The form itself describes the supported combinations and fallbacks.

The source selector, missing-data behavior and live calculations are unchanged. This update does not make merged station data accessible to the review tool. Test with a selected live Tempest source after import; the automated checker may still render the no-data message.

Implementation references: [Shared markup](https://help.trmnl.com/en/articles/13216853-reusing-markup-with-shared), [view wrapper](https://trmnl.com/framework/docs/3.4/view), [title bar](https://trmnl.com/framework/docs/3.4/title_bar), [responsive utilities](https://trmnl.com/framework/docs/3.4/responsive).

### RC8 — Quarter-view fixes

- X quarter current temperature reduced one native size step for each character tier (minus sign counted).
- X landscape quarter: smaller header/icon, content-sized rows and side-by-side forecasts. Forecast details use a compact native label tier and wrap within each day.
- X portrait quarter: Both puts solar/brightness and lightning on separate full-width rows.
- Full and half templates, OG rules, settings and live-data calculations are unchanged from RC7.

Rerun trmy with default settings and Both, with the footer shown, in both X orientations. Local checks do not establish visual approval.

### RC7 — Checker fixes

- Use framework size selectors (`screen--md` / `screen--lg`) in all four views, including footer visibility. This includes the 1-bit OG (`screen--og_png`), which previously missed the OG layout rules.
- Partial views now use native `value`, `label` and `title` elements with responsive `lg:` steps. Removed custom Arial, font-size, font-weight and line-height overrides from partial CSS.
- X portrait half-vertical forecasts use larger native typography and compact, top-aligned rows instead of vertically centered content in tall boxes.
- X landscape half-horizontal joins current and supplementary rows more closely; forecast details use a larger native label step.
- Related settings are grouped under Display. Existing setting keys, defaults and data calculations are unchanged.

Import RC7 and rerun trmy, including 1-bit OG partial views, both footer states, X portrait half-vertical and X landscape half-horizontal. Local structural/HTML checks do not replace TRMNL renderer approval.

### RC6 — Checker fixes

- Removed all viewport-width 1000px enlargement blocks from partial views. Those blocks measured the whole device, not the mashup slot, and oversized icons, grid columns and text.
- Replaced literal partial-view pixel font sizes with framework font-size tokens; X receives a device-scoped label tier. Three/four-character partial temperatures use a smaller value tier, counting the minus sign.
- OG half-horizontal reserves more room between current and secondary readings and uses smaller current-temperature tiers.
- OG quadrant reserves forecast height above the footer, compacts forecast detail text and limits header artwork height.
- Removed unsupported cqw height utility classes from full view; supported width classes and explicit portrait CSS remain.

Live source selection, defaults, translations, pressure conversion, lightning age checks and footer choices remain unchanged. No demo activation has been added. The selector's documented Recipe fork requirement still applies; do not promise no-fork installation until verified with TRMNL.

Validation: Liquid/YAML syntax, CSS structure, removal of viewport triggers, unchanged live-data preparation and HTML render regression checks. Hosted trmy review and physical-device visual verification must be rerun; this package is not represented as already approved by the checker.

### RC5 — Release notes

- Default plugin name: **Tempest Enhanced**; the RC version was tracked in the original README and archive filename.
- OG full-screen main weather icon retains the accepted 20% reduction (22cqw to 17.6cqw).
- Optional information defaults to **None**. The experimental full-screen Both change is not included: full-screen OG and X landscape show only solar/brightness for Both; X portrait retains combined readings.
- All temperatures, conditions, timestamps and optional readings use the selected native Tempest source. No summer fixture, frozen clock or forced demo selections are included.
- Expanded About This Plugin description for the public Recipe page, including setup instructions and source dependency.

### RC4 — Accepted layouts and final adjustments

#### Final RC4 adjustment

OG quarter current weather icon reduced a further 6% (109.44 to 102.8736 CSS px). Other layouts retain the accepted RC3 behaviour. Live readings and user-selected options remain unchanged.

#### RC4 layout updates

Incorporates Summer Test 4 layout adjustments: X full-screen main temperatures use 220/170/128 px for 1/2/3+ characters including minus; updated current weather icon sizes and vertical position; X landscape half-horizontal lightning aligns with sunset; portrait half-horizontal description increased one font step. All weather readings and user selections come from the native live source. No demo fixture or forced demo settings.

#### Accepted portrait layouts

X portrait layouts were visually reviewed by the author through test13. Full view includes a condition caption below the main icon. Half-horizontal uses main/supplementary above today/tomorrow, with continuous separators. Half-vertical stacks lightning below solar information. Quarter allows the current condition caption to wrap.

At this stage, the release candidate used live native Tempest data only; settings remain user-controlled. The separate Summer Demo package is synthetic and must not replace the live recipe. The supplied icon is included at `assets/plugin-icon.png`; upload/select it in TRMNL recipe settings.
