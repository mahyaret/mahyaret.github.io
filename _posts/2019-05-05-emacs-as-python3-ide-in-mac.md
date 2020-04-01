---
layout: post
title: Emacs as Python3 IDE in Mac
date: '2019-05-05T12:22:00.000-04:00'
author: Mahyar
tags:
- Emacs
- Python
- Machine Learning
modified_time: '2019-07-15T21:16:02.432-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-869650632199443377
blogger_orig_url: http://www.etedal.net/2019/05/emacs-as-python3-ide-in-mac.html
---


Install the following using your preferred method:  
```  
pip3 install rope jedi importmagic autopep8 flake8  
```
  
In Emacs:  
```  
M-x package-install RET elpy RET  
M-x package-install RET exec-path-from-shell RET  
M-x package-install RET pyenv RET  
M-x package-install RET anaconda-mode RET  
```
Edit `.emacs` as following:  
``` 
(elpy-enable)  
(when (memq window-system '(mac ns x))  
    (exec-path-from-shell-initialize))  
(add-hook 'python-mode-hook 'anaconda-mode)  
(setenv "WORKON\_HOME" "/anaconda3/envs")  
(pyvenv-mode 1)  
```  
Restart your emacs and enjoy using the best Python IDE  
  
Use `M-x pyvenv-workon` to switch between anaconda environments
