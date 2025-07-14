---
layout: post
title: Minimal vim + tmux + vim LSP 
date: '2025-07-14T01:10:00.002-04:00'
author: Mahyar
tags:
- vim
- tmux
---

I'm recently started going back and forth between Vim and VSCode. I code mostly in Python and C++. 

## Installation

1. I know title says "minimal" in the title but sorry `gruvbox` theme is just for me! Here is how you install it:
```
git clone https://github.com/morhetz/gruvbox.git ~/.vim/pack/themes/start/gruvbox
```

2. add the following to your `~/.vimrc`:
```
syntax enable
set background=dark " or 'light'
colorscheme gruvbox
```

3. remember that in your `~/.bashrc` to enable the 256color mode:
```
export TERM=xterm-256color
```

4. now lets install clangd as VimLAP using
```
sudo apt install clangs
```

5. install it for vim
 ```
mkdir -p ~/.vim/pack/lsp/start
```

6. clone the repo
```
git clone https://github.com/prabirshrestha/vim-lsp.git ~/.vim/pack/lsp/start/vim-lsp
```

7. copy the following into `~/.vimrc`:
```
if executable('clangd')
  au User lsp_setup call lsp#register_server({
        \ 'name': 'clangd',
        \ 'cmd': {server_info->['clangd']},
        \ 'whitelist': ['c', 'cpp', 'objc', 'objcpp'],
        \ })
endif
```

8. you can check the status using `:LspStatus`.



## Shortcuts
### vim
shortcuts for navigating `:Ex` in vim:

| Action              | Keybinding           |
| ------------------- | -------------------- |
| Move to next window | `Ctrl + w`, then `w` |
| Move left           | `Ctrl + w`, then `h` |
| Move right          | `Ctrl + w`, then `l` |
| Move up             | `Ctrl + w`, then `k` |
| Move down           | `Ctrl + w`, then `j` |


open a file: `:e path/to/file.cpp`

shortcuts for clangd:
- `gd` to jump to definition
- `gr` to list usages
- `K` to see docs
- `<leader>rn` to rename

### tmux
restart everything: `tmux kill-server`

shortcut for navigating in tmux: 

1. `tmux` → start
2. `Ctrl + b`, `%` / `"` → split
3. `Ctrl + b`, arrow → move
4. `Ctrl + b`, `d` → detach
5. `tmux attach` → reattach

Resize a tmux pane (split window) 

you can add mouse control to `~/.tmux.conf` as well: `set -g mouse on`

| Action       | Key Combo               |
| ------------ | ----------------------- |
| Resize left  | `Ctrl + b` → `Ctrl + ←` |
| Resize right | `Ctrl + b` → `Ctrl + →` |
| Resize up    | `Ctrl + b` → `Ctrl + ↑` |
| Resize down  | `Ctrl + b` → `Ctrl + ↓` |


`Ctrl + b  [` for scrolling


| Action                      | Shortcut             |
| --------------------------- | -------------------- |
| Zoom pane (fullscreen)  | `Ctrl + b`, then `z` |
| Unzoom (restore layout) | `Ctrl + b`, then `z` |

