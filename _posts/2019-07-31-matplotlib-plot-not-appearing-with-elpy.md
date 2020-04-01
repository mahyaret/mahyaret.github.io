---
layout: post
title: 'Matplotlib plot not appearing with elpy in Emacs '
date: '2019-07-31T11:22:00.001-04:00'
author: Mahyar
tags:
- Emacs
- Python
modified_time: '2019-07-31T12:37:56.507-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-8246238607515999642
blogger_orig_url: http://www.etedal.net/2019/07/matplotlib-plot-not-appearing-with-elpy.html
---


For solving this, you can use different back-end:  
```  
import matplotlib  
matplotlib.use('TkAgg')  
import matplotlib.pyplot as plt  
```  
Other GUI backends:  

*   `TkAgg`
*   `WX`
*   `QTAgg`
*   `QT4Agg`

Run your code using: `C-u C-c C-c`
