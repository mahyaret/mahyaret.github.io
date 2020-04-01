---
layout: post
title: Fix tmux issue with conda
date: '2019-07-03T10:30:00.001-04:00'
author: Mahyar
tags:
- Jupyter
- Python
modified_time: '2019-07-03T10:35:03.333-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-2001883735173821852
blogger_orig_url: http://www.etedal.net/2019/07/fix-tmux-messing-with-conda.html
---


**[source](https://gist.github.com/ekreutz/995bb95e428358b9efa2b2f80b02143c)**  
**Problem**: When running a conda environment and opening tmux on macOS, a utility called `path_helper` is running again. Essentially, the shell is initialized twice which messes up the `${PATH}` so that the wrong Python version shows up within tmux.  
  
**Solution**  If using bash, edit /etc/profile and add one line. (For `zsh`, edit `/etc/zprofile`)
```
if [ -x /usr/libexec/path_helper ]; then
	PATH="" # <- ADD THIS LINE (right before path_helper call)
	eval `/usr/libexec/path_helper -s`
fi
```
