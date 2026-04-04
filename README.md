# TMUX Configuration Repository



## Overview
This repository contains various configuration files for setting up and customizing TMUX, a terminal multiplexer renowned for its powerful session management features.

## Files

- **tmux.conf**: The main configuration file for TMUX.
- **macos.conf**: Configuration specific to macOS.
- **theme.conf**: Configuration for visual themes.
- **utility.conf**: Miscellaneous utilities for TMUX.
- **statusline.conf**: Customizations for the TMUX status line.

## Usage
1. Clone this repository to your local machine.
2. Symlink the provided `tmux.conf` to your home directory:
   ```bash
   ln -s /path/to/repo/tmux.conf ~/.tmux.conf
   ```
3. (Optional) If you are using macOS, add the `macos.conf` to your TMUX configuration by including it in `tmux.conf`:
   ```
   source-file /path/to/repo/macos.conf
   ```
4. Include other configurations like `theme.conf`, `utility.conf`, and `statusline.conf` where necessary.

## Contribution
Contributions to improve or extend these TMUX configurations are welcome. Open a pull request with your changes and ensure to follow existing coding conventions.

## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Keymap
This repository allows users to set up useful and customizable keymaps in TMUX. Keymaps help you define and manage custom shortcuts to maximize productivity. Below are some examples of common mappings you can include:

- **Split Pane**: Quickly split the current TMUX pane horizontally or vertically using shortcuts. Default examples:
  ```tmux
  bind \ split-window -h
  bind - split-window -v
  ```
- **Switch Panes**: Navigate between panes seamlessly with easy-to-remember shortcuts. Default examples:
  ```tmux
  bind h select-pane -L
  bind l select-pane -R
  bind j select-pane -D
  bind k select-pane -U
  ```
- **Resize Panes**: Resize the current pane with key combinations:
  ```tmux
  bind -r < resize-pane -L
  bind -r > resize-pane -R
  bind -r + resize-pane -U
  bind -r - resize-pane -D
  ````
Users are encouraged to modify these keymaps within `tmux.conf` file according to their preferences.

---
**Note:** Ensure you have TMUX installed on your system. For installation instructions, visit the TMUX [official documentation](https://github.com/tmux/tmux).

