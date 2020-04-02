---
layout: post
title: Common Lisp IDE
date: '2018-11-05T22:15:00.001-05:00'
author: Mahyar
tags:
- Linux
- Emacs
- debian
- Common Lisp
modified_time: '2018-11-05T22:20:50.894-05:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-129707403757893771
blogger_orig_url: http://www.etedal.net/2018/11/common-lisp-ide.html
---


Best resource for Common Lisp can be found here: [https://github.com/norvig/paip-lisp](https://github.com/norvig/paip-lisp)  
  
Emacs  
```  
sudo apt-get install emacs  
```   
SBCL  
  
- Download from here: [http://www.sbcl.org/platform-table.html](http://www.sbcl.org/platform-table.html)  
- `sudo ./install.sh`  
  
Slime  
- create .emacs  in your home folder.  
 - paste the following to it:  
 ```
(require 'package)
(let* ((no-ssl (and (memq system-type '(windows-nt ms-dos))
                    (not (gnutls-available-p))))
       (proto (if no-ssl "http" "https")))
  ;; Comment/uncomment these two lines to enable/disable MELPA and MELPA Stable as desired
  (add-to-list 'package-archives (cons "melpa" (concat proto "://melpa.org/packages/")) t)
  ;;(add-to-list 'package-archives (cons "melpa-stable" (concat proto "://stable.melpa.org/packages/")) t)
  (when (< emacs-major-version 24)
    ;; For important compatibility libraries like cl-lib
    (add-to-list 'package-archives (cons "gnu" (concat proto "://elpa.gnu.org/packages/")))))
(package-initialize)
;; Setting lisp system
(setq inferior-lisp-program "/usr/local/bin/sbcl")
(setq slime-contribs '(slime-fancy))
```
- then in emacs:  
```
M-x package-refresh-contents
M-x package-install RET slime RET
```

For running and quiting LISP:
```
start -> M-x slime
stop -> , sayoonara
```
