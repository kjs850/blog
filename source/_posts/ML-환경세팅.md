---
title: ML 환경세팅
---
date: 2019-03-08 10:38:22

## 학습교재
나의 첫 머신러닝/딥러닝

## git clone
https://github.com/wikibook/machine-learning

## conda를 이용한 환경 구성
```bash
jake.ko  ~/Dev/machine-learning   master  ll
total 16
drwxr-xr-x  28 jake.ko  staff   896  3  7 18:41 ..
drwxr-xr-x   4 jake.ko  staff   128  3  7 18:41 data
drwxr-xr-x  27 jake.ko  staff   864  3  7 18:41 jupyter_notebook
-rw-r--r--   1 jake.ko  staff  3425  3  7 18:41 wikiml_mac.yml
drwxr-xr-x   7 jake.ko  staff   224  3  7 18:41 .
-rw-r--r--   1 jake.ko  staff  3475  3  7 18:41 wikiml_win.yml
drwxr-xr-x  13 jake.ko  staff   416  3  7 18:46 .git
 jake.ko  ~/Dev/machine-learning   master  vi wikiml_mac.yml
 jake.ko  ~/Dev/machine-learning   master  conda env create -f wikiml_mac.yml
Solving environment: done

==> WARNING: A newer version of conda exists. <==
  current version: 4.5.11
  latest version: 4.6.7
Please update conda by running
    $ conda update -n base -c defaults conda

Downloading and Extracting Packages
xz-5.2.3             | 253 KB    | ############################################################ | 100%
certifi-2018.4.16    | 142 KB    | ##################

....

  Found existing installation: numpy 1.14.1
    Uninstalling numpy-1.14.1:
      Successfully uninstalled numpy-1.14.1
Successfully installed autokeras-0.2.1 numpy-1.14.5 pillow-5.2.0 torch-0.4.0 torchvision-0.2.1
#
# To activate this environment, use
#
#     $ conda activate wikiml
#
# To deactivate an active environment, use
#
#     $ conda deactivate
 jake.ko  ~/Dev/machine-learning   master 

```

## 실행/종료
conda activate wikiml

jupyter notebook

conda deactivate



tags:
