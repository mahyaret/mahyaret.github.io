---
layout: post
title: Use Azure as your Jupyter notebook Server
date: '2019-03-23T13:37:00.001-04:00'
author: Mahyar
tags:
- Jupyter
- Linux
- Azure
- Kaggle
- Deep Learning
- Machine Learning
- XGBoost
modified_time: '2019-04-25T23:09:47.422-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-2629226378369394941
blogger_orig_url: http://www.etedal.net/2019/03/use-azure-as-your-jupyter-notebook.html
---


Make sure to follow the steps from this post to setup your Azure Virtual Machine:[http://www.etedal.net/2019/03/setting-up-azure-nc6-for-kaggle.html](http://www.etedal.net/2019/03/setting-up-azure-nc6-for-kaggle.html) 
  
Setup Jupyter remote ssh connection:

**On Azure**
```
jupyter notebook --no-browser --port=2001
```

**On your machine** 
```
ssh -N -f -L localhost:2002:localhost:2001 remoteuser@remotehost
```

**(Optional if you use mosh instead)** 
```
mosh -ssh "ssh -N -f -L localhost:2002:localhost:2001" remoteuser@remotehost  
```
**On your browser**
```
 localhost:2002
 ```
