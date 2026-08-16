<div align="center">

# TMUX CONFIG

Tokyo Night · Vi keys · Popups · Cross-platform

![tmux](https://img.shields.io/badge/tmux-1BB91F?style=for-the-badge&logo=tmux&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/macOS-000000?style=for-the-badge&logo=apple&logoColor=white)
![Vim](https://img.shields.io/badge/Vim-019733?style=for-the-badge&logo=vim&logoColor=white)
![Tokyo%20Night](https://img.shields.io/badge/Tokyo%20Night-7aa2f7?style=for-the-badge)
![lazygit](https://img.shields.io/badge/lazygit-F05032?style=for-the-badge&logo=git&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

</div>

A personal tmux setup with a **Tokyo Night** statusline, Vim-style pane navigation, true-color terminals, and popup workflows for lazygit and a scratch `devbox` session. Prefix is **`Ctrl-t`**.

### Features

- **Prefix**: `Ctrl-t` instead of the default `Ctrl-b`.
- **Vi mode**: copy-mode and pane movement follow Vim (`h` `j` `k` `l`).
- **Theme**: Tokyo Night (night palette) with a powerline-style statusline — session, user, window path, hostname.
- **Splits**: `|` and `-` open panes in the current working directory.
- **Popups**: lazygit overlay (`prefix + g`) and a floating `devbox` terminal (`Alt-t`).
- **macOS**: `macos.conf` is sourced automatically on Darwin (clipboard + undercurl).
- **True color**: `xterm-256color` with `Tc` overrides.

---

### 1. Prerequisites

| Requirement     | Notes                                      |
| --------------- | ------------------------------------------ |
| **tmux**        | 3.0+ recommended (undercurl on macOS)      |
| **Git**         | Clone / updates                            |
| **A Nerd Font** | Powerline glyphs (`` `` ``) in the bar |
| **lazygit**     | Optional — used by the `g` popup           |
| **xdg-open**    | Linux — open the current pane directory    |

> **Note**: On macOS, install [reattach-to-user-namespace](https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard) if you need clipboard access from tmux.

```bash
# Fedora
sudo dnf install tmux

# Debian / Ubuntu
sudo apt install tmux

# macOS
brew install tmux
```

---

### 2. Installation

This repo is meant to live at `~/.config/tmux` (XDG). The main file is `tmux.conf`.

#### 2.1 Clone

```bash
git clone git@github.com:smile-ko/tmux-config.git ~/.config/tmux
```

If you already keep configs in `~/.config/tmux`, clone elsewhere and copy or symlink the files.

#### 2.2 Point tmux at this config

**Option A — XDG (recommended)**  
tmux 3.2+ loads `~/.config/tmux/tmux.conf` automatically. No extra symlink.

**Option B — classic `~/.tmux.conf`**

```bash
ln -sf ~/.config/tmux/tmux.conf ~/.tmux.conf
```

If you use Option B, either keep the `source ~/.config/tmux/...` paths as they are, or clone into `~/.config/tmux` so those paths resolve.

#### 2.3 Reload

Inside a tmux session:

```text
prefix (Ctrl-t) then r
```

Or from a shell:

```bash
tmux source-file ~/.config/tmux/tmux.conf
```

---

### 3. Project Structure

```
~/.config/tmux/
├── tmux.conf          # Prefix, keybindings, terminal, copy-mode
├── theme.conf         # Tokyo Night colours, pane borders, clock
├── statusline.conf    # Powerline status bar (session, user, path, host)
├── utility.conf       # lazygit popup + Alt-t devbox terminal
├── macos.conf         # Darwin clipboard + undercurl (sourced on macOS only)
└── README.md
```

`tmux.conf` sources the others in this order: `theme.conf` → `macos.conf` (Darwin) → `statusline.conf` → `utility.conf`.

---

### 4. Keybindings

Prefix is **`Ctrl-t`**. Keys marked *no prefix* work without it.

#### 4.1 General

| Key              | Action                                      |
| ---------------- | ------------------------------------------- |
| `Ctrl-t`         | Prefix                                      |
| `prefix` + `r`   | Reload `tmux.conf`                          |
| `prefix` + `o`   | Open current pane path (`xdg-open` on Linux)|
| `prefix` + `e`   | Kill all panes except the current one       |
| `prefix` + `g`   | lazygit popup (80% × 80%)                   |
| `Alt-t`          | Toggle floating `devbox` session (*no prefix*) |

#### 4.2 Panes

| Key                    | Action                                      |
| ---------------------- | ------------------------------------------- |
| `prefix` + `\|`        | Split horizontally (same cwd)               |
| `prefix` + `-`         | Split vertically (same cwd)                 |
| `prefix` + `h` `j` `k` `l` | Move left / down / up / right           |
| `prefix` + `Ctrl-h` `j` `k` `l` | Resize (5 cols / 4 rows)           |
| `Alt-1` … `Alt-9`      | Select pane 0–8 (*no prefix*)               |

#### 4.3 Windows

| Key                         | Action                         |
| --------------------------- | ------------------------------ |
| `Ctrl-Shift-Left`           | Swap window left, then select  |
| `Ctrl-Shift-Right`          | Swap window right, then select |

#### 4.4 Copy mode (Vi)

| Key                         | Action                                      |
| --------------------------- | ------------------------------------------- |
| `prefix` + `[`              | Enter copy mode                             |
| `y` (in copy-mode-vi)       | Yank and cancel (`pbcopy` + “Copied!”)      |

> On Linux, `y` still pipes through `pbcopy`. Point that command at `wl-copy` or `xclip` if you are not on macOS.

---

### 5. Statusline & Theme

The bar follows **Tokyo Night night** ([folke/tokyonight.nvim](https://github.com/folke/tokyonight.nvim)):

| Element        | Colour        | Role                          |
| -------------- | ------------- | ----------------------------- |
| Session        | `#7aa2f7`     | Left segment                  |
| User           | `#3b4261`     | After session                 |
| Active window  | Blue on gutter| Index + basename of pane path |
| Inactive window| Dim `#a9b1d6` | Index + basename of pane path |
| Hostname       | `#7aa2f7`     | Right segment                 |
| Status bg      | `#1a1b26`     | Bar background                |

Pane borders use `#3b4261` (inactive) and `#7aa2f7` (active). Inactive panes are dimmed (`#565f89`).

Install a Nerd Font (e.g. **JetBrainsMono Nerd Font**, **MesloLGS NF**) and set it in your terminal so the powerline separators render correctly.

---

### 6. Utilities

#### 6.1 lazygit popup

`prefix` + `g` opens [lazygit](https://github.com/jesseduffield/lazygit) in a popup rooted at `#{pane_current_path}`.

```bash
# Fedora
sudo dnf install lazygit

# macOS
brew install lazygit
```

#### 6.2 Floating `devbox` terminal

`Alt-t` attaches to (or creates) a session named `devbox` inside an 85% × 80% popup. Press `Alt-t` again from inside that session to detach.

Useful as a scratch shell without leaving the current layout.

---

### 7. macOS

On Darwin, `tmux.conf` sources `macos.conf`:

- `reattach-to-user-namespace` for clipboard / user namespace
- Undercurl and underline colour overrides (tmux 3.0+)

Linux uses `xdg-open` for `prefix` + `o`. On macOS, switch that bind to `open` if you want Finder:

```tmux
bind o run-shell "open '#{pane_current_path}'"
```

---

### 8. Settings worth knowing

| Option              | Value              | Why                                      |
| ------------------- | ------------------ | ---------------------------------------- |
| `prefix`            | `C-t`              | Frees `Ctrl-b`                           |
| `mode-keys`         | `vi`               | Vim copy / navigation                    |
| `history-limit`     | `64096`            | Long scrollback                          |
| `escape-time`       | `10`               | Faster Vim / Neovim                      |
| `focus-events`      | `on`               | Editors detect focus                     |
| `repeat-time`       | `500`              | Repeat pane move / resize                |
| `set-titles`        | `on` (`#T`)        | Terminal title follows pane              |
| `default-terminal`  | `xterm-256color`   | 256 colour + true color (`Tc`)           |

---

### 9. Customization

| Goal                    | File                 |
| ----------------------- | -------------------- |
| Keys, prefix, splits    | `tmux.conf`          |
| Colours, pane styles    | `theme.conf`         |
| Status bar layout       | `statusline.conf`    |
| Popups / extra binds    | `utility.conf`       |
| macOS-only behaviour    | `macos.conf`         |

After edits:

```bash
tmux source-file ~/.config/tmux/tmux.conf
```

---

### 10. Troubleshooting

#### Config not loading

Confirm tmux is reading this tree:

```bash
tmux display-message -p '#{config_files}'
ls ~/.config/tmux/tmux.conf
```

If you use `~/.tmux.conf`, it must source or match the paths in this repo (`~/.config/tmux/...`).

#### Broken statusline glyphs

The bar uses Nerd Font / powerline symbols. Set a Nerd Font in the terminal emulator and restart it.

#### lazygit popup does nothing

Install `lazygit` and ensure it is on `PATH` inside tmux (`echo $PATH`).

#### Copy with `y` does not reach the system clipboard

`copy-mode-vi y` runs `pbcopy`. On Linux, replace it in `tmux.conf` with `wl-copy` (Wayland) or `xclip -selection clipboard` (X11).

#### Prefix conflicts with the terminal

`Ctrl-t` is the prefix. If the terminal or an editor already uses it, change `prefix` in `tmux.conf`.

---

### 11. License

MIT. See the repository for details.
