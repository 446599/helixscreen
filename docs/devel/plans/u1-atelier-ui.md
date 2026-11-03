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

## Build and install

Build the U1 package with `make package-snapmaker-u1` on a configured Linux Docker build
host. For a directly attached development printer, `make deploy-snapmaker-u1` uses the
existing SSH deploy path and restarts the app; set `SNAPMAKER_U1_HOST` first. Do not use
the standalone installer on a PAXX firmware-managed install. PAXX owns the pinned
`extended-pkg` package under `/oem/apps/helixscreen`; package upgrades must go through
PAXX's Snapmaker Components touchscreen flow using its HelixScreen package artifact.
On a non-firmware-managed U1 install, follow `docs/user/guide/install-u1.md` and deploy
the release archive to `/userdata/helixscreen/`.
