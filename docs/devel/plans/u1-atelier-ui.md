# U1 Atelier UI

## Before and after

The 480x320 first-run language step currently spends half of its content area on a
cycling welcome label, then puts a narrow language picker inside a bordered card. The
Atelier pass uses the full content width for the language list, gives each language a
large touch row, and reduces the wizard header's padding so the choice area has room.

The new U1 home seed starts with printer status and core temperatures on the home page.
The fan stack, temperature graph, and tips are no longer part of the initial compact
layout. They remain available in the widget catalog, alongside the printer's existing
AMS/ACE, print, camera, motion, mesh, settings, and macro features. A compact panel with
no saved theme preference now starts with the U1 Atelier palette; an explicit theme
choice always takes precedence.

## Preview

For XML/theme-only iteration, start the native test app with the compact size and mock U1:

```bash
HELIX_MOCK_PRINTER=snapmaker_u1 HELIX_THEME=u1-atelier ./build/bin/helix-screen --test --size tiny -vv
```

Complete or reset the wizard to inspect all setup steps. `HELIX_THEME` is optional once
the compact-screen default is in effect. The U1 preset also loads its compact home seed.

## V2: quieter surfaces

The first preview still felt too busy, so v2 removes the framed surface around the
language list and drops row dividers entirely. Selection is a low-opacity elevated
fill, while the wizard progress and subtitle recede behind the title and content.
The primary action uses the theme accent. The Atelier palette moves closer to black,
uses softer secondary text, raises border radius to 10, lowers border opacity to 10, and keeps shadows off.

The compact U1 home seed continues to suppress the fan stack, temperature graph, and
tips. Its initial view stays focused on print state and heater metrics; optional
widgets remain available through the catalog.


## V3: Claude palette + minimal skeuomorphism

Henry asked for Claude.ai-like warm cream paper with terracotta accents instead of the
dark teal industrial look. Light is the intended default for U1 Atelier (snapmaker_u1 /
HELIX_THEME=u1-atelier when `/dark_mode` is unset). Dark keeps a warm charcoal alternate.

Theme knobs turn soft elevation back on (`shadow_intensity` 16, `shadow_opa` 32,
`shadow_offset_y` 3, `border_radius_size` Rounded/4) so primary buttons, selected language
chips, and cards can read as lightly raised — minimal skeuomorphism without heavy chrome.
Language selection uses a raised card-fill chip with the theme shadow; unselected rows stay
flat. `ui_card` no longer hard-zeros shadow when the active theme enables one.

## V4: U1 structure and hierarchy

The U1 compact home now gives print state the upper five of eight grid rows, then places
nozzle and bed temperatures together in the remaining row. The active-print percentage is
larger, and compact temperature values use the medium readout size. Printer imagery, tips,
fan stacks, and the temperature graph stay off the default U1 home. The widget catalog and
Filament destination retain the optional features.

On U1, navigation now presents Home, Files, Controls, Filament, Settings, then Advanced.
Panel IDs and their behavior stay stable; Files moves into the second, easiest-to-reach
position. Compact body and heading fonts step up, while the Files, Motion, and temperature
surfaces use more breathing room. Existing U1 installs that still have enabled stock
`tips`, `fan_stack`, or `printer_image` anchors are reset once to the U1 seed and marked in
printer settings as `u1_home_layout_version: 1`; other saved home layouts are kept.

## Build and install

Build the U1 package with `make package-snapmaker-u1` on a configured Linux Docker build
host. For a directly attached development printer, `make deploy-snapmaker-u1` uses the
existing SSH deploy path and restarts the app; set `SNAPMAKER_U1_HOST` first. Do not use
the standalone installer on a PAXX firmware-managed install. PAXX owns the pinned
`extended-pkg` package under `/oem/apps/helixscreen`; package upgrades must go through
PAXX's Snapmaker Components touchscreen flow using its HelixScreen package artifact.
On a non-firmware-managed U1 install, follow `docs/user/guide/install-u1.md` and deploy
the release archive to `/userdata/helixscreen/`.
