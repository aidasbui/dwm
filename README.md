# dwm (personal fork)

Personal fork of [dwm](https://dwm.suckless.org), the dynamic window manager
for X. Tracks `upstream` (`git@git.suckless.org/dwm`) as a separate remote so
upstream changes can still be pulled in; this fork carries three source
patches plus local `config.def.h` customization on top.

## Patches applied

- **vanitygaps** (`vanitygaps.c`) - configurable gaps between tiled windows.
  - `gappih`/`gappiv`/`gappoh`/`gappov` in `config.def.h` control inner/outer
    gap size (currently 8px inner, 12px outer).
  - `MODKEY+Mod4+0` toggles gaps on/off, `MODKEY+Mod4+Shift+0` resets to
    default gap size.
- **movestack** (`movestack.c`) - reorder the current client within the
  stack without leaving keyboard focus.
  - `MODKEY+Ctrl+j` / `MODKEY+Ctrl+k` move the focused client down/up the
    stack (`h`/`l` are mapped the same as `k`/`j` respectively).
- **cfact** (`dwm.c`: `Client.cfact`, `setcfact()`) - per-client resize
  factor, lets one stacked client take a larger/smaller share of its area
  independent of the shared `mfact`.
  - `MODKEY+Shift+h` / `MODKEY+Shift+l` shrink/grow the focused client's
    factor, `MODKEY+Shift+o` resets it to `1.0`.

## Local config changes (not upstream patches)

- Colors in `config.def.h` (`col_gray1..4`, `col_border`) match the
  [dimmed-monokai](https://github.com/aidasbui/dimmed-monokai.nvim) palette
  used across kitty/tmux/nvim, so the WM border/bar match the terminal theme.
- `termcmd` set to `kitty` (was `st`).
- New keybind: `MODKEY+Shift+equal` spawns `flameshot gui` for screenshots.
- New layout: `col` (bottom entry in `layouts[]`), bound to `MODKEY+c`.
- Added `togglefullscreen()` (not bound to a key by default - reserved for
  future use).
- `quit` keybind (`MODKEY+Shift+q`) moved earlier in the `keys[]` array; no
  behavior change.

## Build

Standard suckless build, no extra config needed beyond what's already in
`config.mk`:

    make clean install

Requires the usual Xlib dev headers (`libx11-dev`, `libxft-dev`,
`libxinerama-dev`, `libxrandr-dev`, `libxext-dev` on Debian) - already listed
in the dotfiles repo's `packages.txt`.

## Updating from upstream

    git fetch upstream
    git merge upstream/master

Conflicts are most likely in `config.def.h` and `dwm.c` given the patches
touch both; resolve keeping the patch hunks above intact.
