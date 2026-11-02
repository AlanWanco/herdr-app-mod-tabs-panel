# Tabs (panel kept open) — a brief

Copy Herdr's shipped `tabs` mod (`~/.config/herdr-app/mods/tabs/`) into `mods/tabs-panel/` and remove
exactly one behaviour: the per-space memory of the side panel.

## What it builds

- `main.js` is the shipped file with `syncPanel(space, panel, body, enabled)` replaced by an empty
  function and its call dropped (it is the only caller). Everything else — tab pills, the `+` menu,
  the Files/Changes panel buttons, window buttons, `pressed`/scroll handling — stays byte for byte.
- `mod.json` keeps the shipped shape: `{ "place": "none", "title": "Tabs" }`.

## Install shape

The user copies the folder to `~/.config/herdr-app/mods/tabs-panel/` and edits a **cloned** layout so
the tab-bar block's `content.mod` is `tabs-panel`. Shipped layouts are replaced on start, so a clone
is the only place the edit survives.

## Built from

`gpui-kit`, `gpui-base`, `herdr` (`spaces`, `panes`, `run`, `openOverlay`, `theme`, `window`, `layout`,
`settings`). Assets stay in the shipped `tabs` and `workspace-chrome` folders.

## Watch out

- Clone, do not edit `mods/tabs`: Herdr replaces shipped mods at every start and moves an edited one
  to `tabs-edited`, which then diverges anyway.
- The panel buttons call `layout.select` / `layout.show` / `layout.hide`; without `syncPanel` nothing
  fights them.
- Keeping the shipped `tabs` folder installed matters only for its SVG assets.

## Done when

Switch agents across spaces with the panel open: it stays open, on the same tab. Clicking Files or
Changes still toggles it.
