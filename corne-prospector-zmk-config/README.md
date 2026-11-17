# Typeractive Corne + Prospector dongle (ZMK)

ZMK config for a **Typeractive Corne Wireless** (6-column, 42 keys) with
**nice!nano v2** controllers, **nice!view** displays, and a
**Prospector** dongle (XIAO nRF52840 + round LCD) as the central.

| Device | Role | Board | Shield |
|---|---|---|---|
| Left half | peripheral | `nice_nano//zmk` | `corne_left nice_view_adapter nice_view` |
| Right half | peripheral | `nice_nano//zmk` | `corne_right nice_view_adapter nice_view` |
| Prospector | central, USB to PC | `xiao_ble//zmk` | `corne_dongle prospector_adapter` |

## Get the firmware
1. Push this repo to GitHub.
2. **Actions** tab -> *Build ZMK firmware* -> open the latest run.
3. Download the **firmware** artifact and unzip it.

## Flash (first time)
Double-tap reset on each board so a USB drive appears, then drag the `.uf2` on.
1. `settings_reset-nice_nano-zmk.uf2` -> left half, then right half
2. `settings_reset-xiao_ble-zmk.uf2` -> dongle
3. `corne_dongle_prospector_adapter-xiao_ble-zmk.uf2` -> dongle
4. `corne_left_nice_view_adapter_nice_view-nice_nano-zmk.uf2` -> left
5. `corne_right_nice_view_adapter_nice_view-nice_nano-zmk.uf2` -> right

Plug the **dongle** into your computer. Both halves connect to it on their own.
Remove the Corne from any Bluetooth device lists on your computer; it is only
the dongle now. File names may differ slightly: match them by the names above.

## Customize
- Keys: `config/corne.keymap` (only the dongle reads it).
- Prospector brightness / sensor options: `config/corne_dongle.conf`.
- Pressing `&bootloader` / `&sys_reset` on the Adjust layer resets the half you pressed it on.

## If the build fails
Open the failed run and check the "Build" step log. The usual causes are
Prospector module / ZMK `main` drifting apart (check the module's README for the
current branch and update `revision:` in `config/west.yml`) or a typo in an edit.
