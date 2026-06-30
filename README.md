# kiro-labwc

The **lightweight Openbox-style edition** of Kiro — labwc, a traditional stacking desktop in the
Kiro Wayland line (sibling to [kiro-hyprland](https://github.com/kirodubes/kiro-hyprland)).

## What it is

A configuration package: the source-of-truth config tree for Kiro's labwc edition. labwc is an
**Openbox-for-Wayland** compositor — **stacking, not tiling**: move/resize/snap-to-edge windows, a
real **right-click root menu**, Openbox "desktops" as workspaces. It's the deliberate *lightweight,
traditional-desktop* member (the niche Raspberry Pi OS picked labwc for), not a keyboard-driven
tiler. It ships the same **waybar + mako + swaybg** shell as kiro-hyprland, so the look matches; only
the compositor (XML) and window-management vocabulary differ.

## What it ships

- `etc/skel/.config/labwc/` — `rc.xml` (keybinds + behaviour, Openbox syntax), `menu.xml` (the
  Kiro right-click menu), `autostart` (session services), `environment` (Wayland env),
  `themerc-override` (Tokyo Night titlebar theme), `keybindings.txt`, `bg/kiro.jpg`, and `scripts/`
  (`set-theme.sh`, `import-gsettings.sh`).
- `etc/skel/.config/waybar/` — the bar (`config.jsonc`, `style.css`, pywal-driven `colors.css`).
- `etc/skel/.config/{mako,hypr}/` — notifications + the hyprlock/hypridle lock pipeline.

## Theming — pywal (incl. the titlebar)

One wallpaper drives every colour. labwc themes window decorations *separately* from the bar (the
Openbox `themerc`), so `set-theme.sh` regenerates **both** the waybar palette **and** the
`themerc-override`, then runs `labwc --reconfigure` to apply the titlebars live. Re-theme with
`~/.config/labwc/scripts/set-theme.sh /path/to/wallpaper.jpg`.

## How to install

```sh
sudo pacman -S kiro-labwc
```

`kiro-labwc` depends on `labwc` + the waybar stack + `python-pywal` (all from `extra`). Pick **Kiro
labwc** at the greeter. **Right-click the desktop** for the menu; workspaces are Openbox **desktops**
(Super+1..9); snap windows with Super+arrows. Press **Super+Ctrl+S** for the keybindings cheat sheet.

A pristine copy of the config is kept at `/usr/share/kiro/kiro-labwc/`.
