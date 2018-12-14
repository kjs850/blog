---
title: mac keras 설치
---
date: 2018-12-14 18:25:58

``` bash
 jake.ko  ~/Dev/keras_talk  sudo pip install virtualenv

 ✘ jake.ko  ~/Dev/keras_talk  virtualenv venv
New python executable in /Users/jake.ko/Dev/keras_talk/venv/bin/python2.7
Also creating executable in /Users/jake.ko/Dev/keras_talk/venv/bin/python
Installing setuptools, pip, wheel...
done.

 jake.ko  ~/Dev/keras_talk  source venv/bin/activate
(venv)  jake.ko  ~/Dev/keras_talk 
(venv)  jake.ko  ~/Dev/keras_talk 

(venv)  jake.ko  ~/Dev/keras_talk  pip install ipython
(venv)  jake.ko  ~/Dev/keras_talk  pip install notebook

## 주피터 노트북을 다음 명령으로 실행시킵니다.

(venv)  jake.ko  ~/Dev/keras_talk  jupyter notebook
[I 18:30:44.774 NotebookApp] Writing notebook server cookie secret to /Users/jake.ko/Library/Jupyter/runtime/notebook_cookie_secret
[I 18:30:45.120 NotebookApp] Serving notebooks from local directory: /Users/jake.ko/Dev/keras_talk
[I 18:30:45.120 NotebookApp] The Jupyter Notebook is running at:
[I 18:30:45.121 NotebookApp] http://localhost:8888/?token=ab851dced4d189daa35e219bfb4abbe28e05686888691d38
[I 18:30:45.121 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 18:30:45.122 NotebookApp]

    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8888/?token=ab851dced4d189daa35e219bfb4abbe28e05686888691d38
[I 18:30:45.366 NotebookApp] Accepting one-time-token-authenticated connection from ::1

(venv) keras_talk $ pip install numpy
(venv) keras_talk $ pip install scipy
(venv) keras_talk $ pip install scikit-learn
(venv) keras_talk $ pip install matplotlib
(venv) keras_talk $ pip install pandas
(venv) keras_talk $ pip install pydot
(venv) keras_talk $ pip install h5py

## pydot은 모델 가시화할 때 필요한 것인데 이를 사용하려면, graphviz가 필요합니다. brew라는 툴을 이용해서 graphviz를 설치하기 위해 brew를 먼저 설치합니다.
(venv) keras_talk $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
(venv) keras_talk $ brew install graphviz


## 딥러닝 라이브러리 설치
(venv) keras_talk $ pip install theano
(venv) keras_talk $ pip install tensorflow

(venv) keras_talk $ pip install keras
```
## 확인

``` bash
import scipy
import numpy
import matplotlib
import pandas
import sklearn
import pydot
import h5py

import theano
import tensorflow
import keras

print('scipy ' + scipy.__version__)
print('numpy ' + numpy.__version__)
print('matplotlib ' + matplotlib.__version__)
print('pandas ' + pandas.__version__)
print('sklearn ' + sklearn.__version__)
print('pydot ' + pydot.__version__)
print('h5py ' + h5py.__version__)

print('theano ' + theano.__version__)
print('tensorflow ' + tensorflow.__version__)
print('keras ' + keras.__version__)

## 결과
scipy 1.1.0
numpy 1.15.4
matplotlib 2.2.3
pandas 0.23.4
sklearn 0.20.1
pydot 1.4.1
h5py 2.8.0
theano 1.0.3
tensorflow 1.12.0
keras 2.2.4
Using TensorFlow backend.
```

## reference
- https://tykimos.github.io/2017/08/07/Keras_Install_on_Mac/
- https://www.tensorflow.org/install/

tags:
