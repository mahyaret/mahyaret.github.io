---
layout: post
title: Minimal Vim + tmux + VimLSP 
date: '2025-07-14T21:10:00.002-04:00'
author: Mahyar
tags:
- vim
- tmux
---

I'm recently started going back and forth between Vim and VSCode. I code mostly in Python and C++. 

1. I know title says "minimal" in the title but sorry `gruvbox` theme is just for me! Here is how you install it:
```git clone https://github.com/morhetz/gruvbox.git ~/.vim/pack/themes/start/gruvbox```
2. add the following to your `~/.vimrc`:
```syntax enable
set background=dark " or 'light'
colorscheme gruvbox```
3. remember that in your `~/.bashrc` to enable the 256color mode:
```export TERM=xterm-256color```
4. now lets install clangd as VimLAP using
```sudo apt install clangs```
5. install it for vim
 ```mkdir -p ~/.vim/pack/lsp/start```
6. ```git clone https://github.com/prabirshrestha/vim-lsp.git ~/.vim/pack/lsp/start/vim-lsp```
7. copy the following into `~/.vimrc`:
```if executable('clangd')
  au User lsp_setup call lsp#register_server({
        \ 'name': 'clangd',
        \ 'cmd': {server_info->['clangd']},
        \ 'whitelist': ['c', 'cpp', 'objc', 'objcpp'],
        \ })
endif```
8. you can check the status using `:LspStatus`.
