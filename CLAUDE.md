# kiro-labwc — Claude project instructions

## Overview
Config package for the **Kiro labwc edition** — the lightweight Openbox-style **stacking** member of
the KIROTUX Wayland line (sibling to [kiro-hyprland](../kiro-hyprland/CLAUDE.md)). Public, open-core,
shipped via `nemesis_repo`. Full research + decisions live in the internal
`Kiro-HQ/Kirotux/study-of-labwc.md`. It completes the named seven-edition lineup.

## Edition spec (the WM-variable matrix)
- **Compositor:** labwc (extra) — Openbox-for-Wayland, **STACKING not tiling** (move/resize/snap/
  maximize; no master-stack/columns/tiling layouts). The line's first non-tiler — deliberate
  lightweight/traditional outlier (study §5; candidate ADR on admitting a stacking member).
- **Config language:** XML in `~/.config/labwc/`: `rc.xml` (binds + behaviour), `menu.xml`
  (right-click root menu — labwc's signature), `autostart` (plain shell), `environment` (env),
  `themerc-override` (titlebar theme). Live reload: `labwc --reconfigure`.
- **Desktop shell:** **waybar + mako + swaybg** (ported from kiro-hyprland). waybar uses
  `wlr/taskbar` (labwc has no native waybar workspace module, like wayfire); desktops switch via
  Super+1..9 / the menu / Super+,. and .. A waybar top-left icon (`` U+F0BAF, nf-md-apps)
  runs `rofi -show drun` — the same command as `SUPER+D`, not a separate launcher backend.
- **Autostart:** the `autostart` shell script; `GTK_A11Y=none waybar` avoids the ~25s at-spi login
  stall (same fix as kiro-river).
- **Theming:** **pywal**, with the labwc twist — `set-theme.sh` regenerates BOTH the waybar palette
  AND the Openbox `themerc-override` (titlebars are a *separate* palette surface), then
  `labwc --reconfigure`.
- **Lock/idle:** hyprlock + hypridle (line-consistent).
- **Dependencies:** all from `extra` (`wlogout` optdepend, chaotic-aur) — **nothing into
  `nemesis_repo`**; the cleanest packaging gate in the line.

## Keybindings
- SUPER grammar in Openbox vocabulary (`<keybind key="W-…">`): CTRL+ALT launchers + SUPER+F1..F12 +
  `kiro-keybindings` on Super+Ctrl+S. Snap-to-edge (Super+arrows) as the poor-man's tiling;
  GoToDesktop/SendToDesktop for the 9 Openbox desktops. **No tiling binds** — there's no tiling.
- `etc/skel/.config/labwc/keybindings.txt` mirrors `rc.xml` (Openbox vocabulary, NOT the tiling
  template). `kiro-keybindings`'s `WM_MAP` already includes `labwc` (fixed 2026-07-01, along with
  the other five KIROTUX Wayland editions missing at the time).

## Patterns / gotchas
- **Two palette surfaces** — the waybar palette and the Openbox `themerc` titlebar theme are
  separate; `set-theme.sh` drives both. Don't ship a riced bar over grey default titlebars.
- **The right-click menu (`menu.xml`) is the character** — lean into the Openbox heritage.
- Config **not yet validated on a real labwc boot** — confirm `<desktops>`, `GoToDesktop`/
  `SendToDesktop`, `SnapToEdge` syntax against labwc 0.20 man pages before the first ISO test.

## Build / delivery
- Source-of-truth for the config; delivered as the `kiro-labwc` package via
  `../KIROTUX-PKG-BUILD/kiro-labwc/build.sh` (public recipe → `~/EDU/nemesis_repo/`). After editing
  here: rebuild the package, then the ISO. See [../CLAUDE.md](../CLAUDE.md) for the full delivery
  architecture.
