# Changelog

All notable changes to **kiro-labwc** are documented here.
Format: one dated entry per day (`YYYY.MM.DD`), newest first.

## 2026.06.30

### What Changed
- **Initial config package** for the Kiro labwc edition — the lightweight Openbox-style member of
  the KIROTUX Wayland line, and its **first stacking (non-tiling)** edition. Completes the named
  seven-edition lineup (hyprland · niri · sway · river · wayfire · dwl · labwc).
- Ships the same waybar + mako + swaybg shell as kiro-hyprland (look/feel match); the SUPER keybind
  grammar is ported onto labwc's Openbox vocabulary (snap-to-edge, desktops, right-click menu).
- **pywal theming, including the titlebars** — `set-theme.sh` regenerates the waybar palette **and**
  the Openbox `themerc-override`, then `labwc --reconfigure` applies the decoration colours live.
- **Right-click root menu** (`menu.xml`) — labwc's signature Openbox feature, Kiro-branded.

### Technical Details
- `etc/skel/.config/labwc/`: `rc.xml` (Openbox `<keybind key="W-…">` binds — CTRL+ALT launchers +
  SUPER+F1..F12 + snap-to-edge as the poor-man's tiling + GoToDesktop/SendToDesktop for the 9
  Openbox desktops + `kiro-keybindings` on Super+Ctrl+S), `menu.xml`, `autostart` (plain shell),
  `environment` (be,us + compose:caps), `themerc-override` (Tokyo Night decorations).
- **No tiling** — window management is Openbox-style (move/resize/snap/maximize); `keybindings.txt`
  is written in Openbox vocabulary, not the tiling template.
- **Shell ported from kiro-hyprland** — waybar uses `wlr/taskbar` (labwc has no native waybar
  workspace module, like wayfire); `GTK_A11Y=none waybar` in autostart avoids the ~25s at-spi login
  stall. `mako` + `style.css` Tokyo Night defaults, overwritten at login by pywal.
- **Lock** = hyprlock + hypridle (line-consistent).
- Everything from `extra` (`wlogout` optdepend from chaotic-aur) — **nothing built into
  `nemesis_repo`**; the cleanest packaging gate in the line.

### Files
- `etc/skel/.config/labwc/{rc.xml,menu.xml,autostart,environment,themerc-override,keybindings.txt,bg/kiro.jpg,scripts/{set-theme.sh,import-gsettings.sh}}`
- `etc/skel/.config/waybar/{config.jsonc,style.css,colors.css}`
- `etc/skel/.config/{mako/config,hypr/{hyprlock,hypridle}.conf}`
- `README.md`, `CLAUDE.md`, `up.sh`, `setup.sh`, `.gitignore`, `kiro.jpg`

### Not yet verified
- The labwc config is **not validated on a real labwc boot** (not installed on the build box) — run
  `labwc --reconfigure` / check against the 0.20 man pages (`labwc-config.5`, `labwc-actions.5`,
  `labwc-theme.5`) on a real session. In particular confirm `<desktops><number>`, `GoToDesktop
  to="N"`, `SendToDesktop`, and `SnapToEdge` against labwc 0.20.
- `kiro-keybindings` / `/kiro-create-keybindings` still need **labwc** added to their WM-detection
  table (known gap, same one the other editions hit).
