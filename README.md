# Kanata Dvorak Configuration with Home Row Modifiers and Polish Diacritics

This configuration provides a streamlined keyboard remapping setup using [Kanata](https://github.com/jtroo/kanata), combining:

* **Dvorak layout** for ergonomic typing
* **Home row modifiers** for efficient key combinations
* **Polish diacritics layer**, toggleable without interfering with modifier behavior
* **Wayland-based `wtype` integration** for seamless Unicode character input

---

## Features

### 1. Dvorak Base Layer

The default layer follows the Dvorak layout with standard remapping for punctuation and symbols:

```
',.py fgcrl /=
aoeui dhtns -\
;qjkxbmwvz
```

---

### 2. Home Row Modifiers

Home row keys serve a dual purpose:

* **Tapped** → input the letter
* **Held** → act as a modifier key

Defined using `tap-hold` with timing thresholds:

| Key | Tap | Hold   |
| --- | --- | ------ |
| a   | a   | LGUI   |
| o   | o   | LALT   |
| e   | e   | LSHIFT |
| u   | u   | LCTRL  |
| h   | h   | RCTRL  |
| t   | t   | RSHIFT |
| n   | n   | LALT   |
| s   | s   | RGUI   |

---

### 3. Polish Diacritics Layer

Activated via the `Caps Lock` key, configured as a dual-role key:

```lisp
(defalias
  caps_toggle (tap-hold 150 200 esc (layer-toggle polish_dia))
)
```

Alternatively, an explicit toggle can be added:

```lisp
(defalias
  toggle_polish (layer-toggle polish_dia)
)
```

---

### 4. Unicode Diacritics (Wayland Only)

Polish characters are typed using the `wtype` command on Wayland:

```lisp
(defalias
  e_ogonek (cmd wtype "ę")
  o_acute  (cmd wtype "ó")
  a_ogonek (cmd wtype "ą")
  s_acute  (cmd wtype "ś")
  l_stroke (cmd wtype "ł")
  z_acute  (cmd wtype "ź")
  c_acute  (cmd wtype "ć")
  n_acute  (cmd wtype "ń")
  z_dot    (cmd wtype "ż")
)
```

These aliases are mapped in the `polish_dia` layer, preserving typing flow and modifier behavior.

---

## Requirements

* Kanata (v1.8.0 or later)
* Wayland session (e.g., Sway, GNOME Wayland)
* `wtype` (for Unicode input)

### Installation (Linux)

```bash
# Arch Linux
sudo pacman -S kanata wtype

# Debian/Ubuntu
sudo apt install kanata wtype
```

---

## Setup

Place the configuration at:

```
~/.config/kanata/config.kbd
```

Run manually using:

```bash
export XDG_RUNTIME_DIR="/run/user/$(id -u)"
kanata -c ~/.config/kanata/config.kbd
```

---

## Layer Overview

### Base Layer (Dvorak + Modifiers)

```
',.py fgcrl /=
aoeui dhtns -\
;qjkxbmwvz
```

### Polish Diacritics Layer (Toggled via Caps Lock)

```
',.py fgcrł /=
ą o ę u i d h t ń ś -\
;qjkŹbmwvŻ
```

Each diacritic key executes a `wtype` command, ensuring compatibility with modern workflows and avoiding dead keys or AltGr combinations.

---

## Summary

This setup provides:

* A comfortable and efficient Dvorak layout
* Modifier keys directly on the home row
* Native Polish diacritic input using Wayland
* A clean toggle system that doesn't interfere with normal typing behavior

It is intended for users who value multilingual support, ergonomic efficiency, and compatibility with modern Linux desktops.

---

Would you like a diagram showing the active key mappings or a printable cheat sheet layout?

