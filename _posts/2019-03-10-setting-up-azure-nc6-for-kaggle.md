---
layout: post
title: Setting up Azure NC6 for Kaggle Competitions
date: '2019-03-10T11:04:00.000-04:00'
author: Mahyar
tags:
- Ubuntu
- Kaggle
- Python
- Deep Learning
- Machine Learning
- XGBoost
modified_time: '2019-03-10T11:15:54.948-04:00'
blogger_id: tag:blogger.com,1999:blog-727803219276813688.post-2485655550041964672
blogger_orig_url: http://www.etedal.net/2019/03/setting-up-azure-nc6-for-kaggle.html
---


I have chosen NC6 and Ubuntu 18.04  
  
Install the following using Lambda Stack:  
Deep Learning frameworks: `TensorFlow`, `Keras`, `PyTorch`, `Caffe`, `Caffe 2`  
GPU software: `CUDA`, `cuDNN`, NVIDIA drivers  
Development tools: `git`, `tmux`, `screen`, `vim`, `emacs`, `htop`, `valgrind`, `build-essential`  
Using Kaggle's beta API, you can interact with Competitions and Datasets to download data, make submissions, and more via the command line.   
```
LAMBDA_REPO=$(mktemp) && \
wget -O${LAMBDA_REPO} https://lambdalabs.com/static/misc/lambda-stack-repo.deb && \
sudo dpkg -i ${LAMBDA_REPO} && rm -f ${LAMBDA_REPO} && \
sudo apt-get update && sudo apt-get install -y lambda-stack-cuda
sudo reboot
pip3 install xgboost
pip3 install kaggle
```  
  
Kaggle  CLI address should be added to the `$PATH`. Find the path and add it to .profile as follows:
```
pip3 show kaggle
```
After editing `~/.profile`, download `kaggle.json` from kaggle.com and:
```
scp ~/Downloads/kaggle.json usrname@AZURE_IP_ADDRESS:/home/username/.kaggle
```
