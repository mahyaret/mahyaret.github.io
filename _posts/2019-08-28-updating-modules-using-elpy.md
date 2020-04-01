---
layout: post
title: Updating modules using Elpy
date: '2019-08-28T14:49:00.000-04:00'
author: Mahyar
tags:
- Emacs
- Python
modified_time: '2019-08-29T09:07:35.854-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-1836768702168883271
blogger_orig_url: http://www.etedal.net/2019/08/updating-modules-using-elpy.html
---

When a self written module gets updated, reevaluating the buffer and the module in the python shell inside Emacs/Elpy doesn't get updated. For solving this issue, add the following to your Emacs configuration file:  
```
(defun my-restart-python-console ()  
  "Restart python console before evaluate buffer or region to avoid various uncanny conflicts, like not reloding modules even when they are changed"  
  (interactive)  
  (if (get-buffer "*Python*")  
      (let ((kill-buffer-query-functions nil)) (kill-buffer "*Python*")))  
  (elpy-shell-send-region-or-buffer))  
  
(global-set-key (kbd "C-c C-x C-c") 'my-restart-python-console)  
 ``` 
restart your Emacs run your code using `C-c C-x C-c`  
  
In short, this code has the "if clause" for checking if `*Python*` buffer is open. This will help to be able to run `C-c C-x C-c` at any time of development even when there is no Python process already open. Another part is `kill-buffer-query-functions` which neglects the prompt for killing the `*Python*` buffer.
