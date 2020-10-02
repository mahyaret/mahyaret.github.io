---
layout: post
title: Vim + tmux + YouCompleteMe in Windows 10
date: '2020-03-26T21:10:00.002-04:00'
author: Mahyar
tags:
- msys2
- vim
- tmux
modified_time: '2020-03-26T21:14:57.289-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-4113662340949343241
blogger_orig_url: http://www.etedal.net/2020/03/vim-tmux-youcompleteme-in-windows-10_26.html
---


I have recently started using Vim after using Emacs for a while. I have Linux machine and a mac laptop at home and a Windows machine at work. I code mostly in Python and C++ and I got frustrated when every time when I switch my machine I have to work in totally different environment. I use CMake to produce Microsoft Visual Studio project files, so I don’t have to use Microsoft Visual Studio itself. Hence, I’ve started using [MSYS2](https://www.msys2.org/).  
In msys2 you can install tmux using:  

    pacman -S tmux

[YouCompleteMe](https://github.com/ycm-core/YouCompleteMe) should be compiled and it is **NOT** compatible with msys2 python or Anaconda. I have installed curl and git using [choco](https://chocolatey.org/docs/installation) in PowerShell. I git cloned YouCompleteMe and went there and ran  

    python install.py --all

remember I had GoLang and NodeJS (`choco install golang` and `choco install nodejs`) and Visual Studio already installed. Then, I copied this folder to my `~/.vim` in msys2. Under `C:\msys64\home\username\.vim\bundle\YouCompleteMe\third_party\ycmd` there is a file named:  
`PYTHON_USED_DURING_BUILDING`  
In this file it refers to the python that is used for compilation. You should chang it to msys compatible path similar to:  
`/C/Users/USER_NAME/AppData/Local/Continuum/anaconda3/envs/CONDA_ENV/python.exe`  

Some useless notes!
-------------------
### Using ConEmu
mintty which is the default shell in MSYS2 does not show the latest commands on the terminal (at least mine :| ) so I have switched to ConEmu which can be downloaded from here:
https://conemu.github.io/

### Speeding up MSYS2:

For some reason MSYS2 was slow on Windows 10 for me, so I did the following:
```
$ mkpasswd -l -c > /etc/passwd
$ mkgroup -l -c > /etc/group
```
Then I edited `/etc/nsswitch.conf` and modifying passwd and group sections to read from “files” instead of “files db”:
```
# Begin /etc/nsswitch.conf
passwd: files
group: files
db_enum: cache builtin
db_home: cygwin desc
db_shell: cygwin desc
db_gecos: cygwin desc
# End /etc/nsswitch.conf
```

### Comparing two files:

If you already have two panes open, you can  
`:diffthis`  
on each of them and then use:  

*   `]c` Go to next block of diff
*   `dp` Push this version of the current block into the other pane
*   `do` Use the block from the other pane in this pane

You can then turn off diff mode in each pane with the vim command  
`:diffoff`  

### Do you really need Caps key?!

*   I use [SharpKeys](https://github.com/randyrants/sharpkeys/releases) to change my `Caps` key to `Ctrl` key, because I barely use caps.
*   For mac you can do this using `System Preferences>>Keyboard>>Modifier Keys`
*   In Gnome you can do this using `Keyboard>>Layouts>>Options>>Ctrl position>>Caps Lock` as `Ctrl`  
    Now that you have mapped `Ctrl` to an easier location you can use `Ctrl+[` instead of `Esc`.

### Anaconda in MSYS2

In case you are interested your Anaconda Python Environments in msys2 add the following to your `~/.bash_profile` (change username and anaconda path to yours)  

    # >>> conda initialize >>>  # !! Contents within this block are managed by 'conda init' !!  eval "$('/c/Users/USER-NAME/anaconda3/Scripts/conda.exe' 'shell.bash' 'hook')"  # <<< conda initialize <<<

### Starting tmux by default

add the following to `~/.bash_profile` or `~/.bashrc` to start terminal or msys2 with tmux by default:  

    if command -v tmux &> /dev/null && [ -z "$TMUX" ]; 
    then    
        tmux attach -t default || tmux new -s default
    fi

### Looking for Fonts?

Here you can find some good fonts:  
[http://mozilla.github.io/Fira/](http://mozilla.github.io/Fira/)  

### My minimal `dotfiles`

Here is my `.vimrc`:  
<script src="https://gist.github.com/mahyaret/f157a7d7a47c618da7f7d098aba60deb.js"></script>
Here is my `.tmux.conf`:
<script src="https://gist.github.com/mahyaret/f06d62ba4bb3f309b4187008c51343cf.js"></script>
