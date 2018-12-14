---
title: anaconda 세팅
---
date: 2018-12-14 17:08:00

## anaconda 기본 세팅
https://www.anaconda.com/ 에서 다운로드 받아서 설치.

```bash
> conda -V
conda 4.5.11

> conda create -n python2.7 python=2.7
Solving environment: done

## Package Plan ##

  environment location: /anaconda2/envs/python2.7

  added / updated specs:
    - python=2.7
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate python2.7
#
# To deactivate an active environment, use
#
#     $ conda deactivate

>conda env list
 # conda environments:
 #
 base                  *  /anaconda2
 python2.7                /anaconda2/envs/python2.7
 
> conda activate python2.7

(python2.7)> python -V
Python 2.7.15 :: Anaconda, Inc.

> conda deactivate
(base)> conda deactivate
>
>

```

## 텐서플로우 환경 만들기
```bash

> conda create -n tensorflow_py3.5 python=3.5

> conda env list
# conda environments:
#
base                  *  /anaconda2
py3.5                    /anaconda2/envs/py3.5
python2.7                /anaconda2/envs/python2.7
tensorflow_py2.7         /anaconda2/envs/tensorflow_py2.7
tensorflow_py3.5         /anaconda2/envs/tensorflow_py3.5

> conda activate tensorflow_py3.5

(tensorflow_py3.5) > export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/tensorflow-0.9.0-py3-none-any.whl

(tensorflow_py3.5) > pip3 install --upgrade $TF_BINARY_URL

Collecting tensorflow==0.9.0 from https://storage.googleapis.com/tensorflow/mac/tensorflow-0.9.0-py3-none-any.whl
  Downloading https://storage.googleapis.com/tensorflow/mac/tensorflow-0.9.0-py3-none-any.whl (25.8MB)
    100% |████████████████████████████████| 25.8MB 1.8MB/s
Collecting protobuf==3.0.0b2 (from tensorflow==0.9.0)
  Downloading https://files.pythonhosted.org/packages/00/8e/9a3feb39d464eb7aacc108e6e6e1f2368ec741821486964c4cd0f41baabb/protobuf-3.0.0b2-py2.py3-none-any.whl (326kB)
    100% |████████████████████████████████| 327kB 2.7MB/s
Requirement already satisfied, skipping upgrade: wheel>=0.26 in /usr/local/lib/python3.7/site-packages (from tensorflow==0.9.0) (0.32.2)
Collecting numpy>=1.10.1 (from tensorflow==0.9.0)
  Downloading https://files.pythonhosted.org/packages/3d/c3/a69406093c9a780a74964f41cd56b06c0346d686a9b3f392d123a663f5e0/numpy-1.15.4-cp37-cp37m-macosx_10_6_intel.macosx_10_9_intel.macosx_10_9_x86_64.macosx_10_10_intel.macosx_10_10_x86_64.whl (24.5MB)
    100% |████████████████████████████████| 24.5MB 1.7MB/s
Collecting six>=1.10.0 (from tensorflow==0.9.0)
  Downloading https://files.pythonhosted.org/packages/73/fb/00a976f728d0d1fecfe898238ce23f502a721c0ac0ecfedb80e0d88c64e9/six-1.12.0-py2.py3-none-any.whl
Requirement already satisfied, skipping upgrade: setuptools in /usr/local/lib/python3.7/site-packages (from protobuf==3.0.0b2->tensorflow==0.9.0) (40.5.0)
Installing collected packages: six, protobuf, numpy, tensorflow
Successfully installed numpy-1.15.4 protobuf-3.0.0b2 six-1.12.0 tensorflow-0.9.0

(tensorflow_py3.5)>

```
## 오류 처리
```bash
(tensorflow_py3.5)  ✘ jake.ko  ~  python
Python 3.5.6 |Anaconda, Inc.| (default, Aug 26 2018, 16:30:03)
[GCC 4.2.1 Compatible Clang 4.0.1 (tags/RELEASE_401/final)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
>>> import tensorflow as tf
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: No module named 'tensorflow'


(tensorflow_py3.5)  jake.ko  ~  pip install tensorflow
Collecting tensorflow
생략...

## 이제 에러 안남..
(tensorflow_py3.5)  jake.ko  ~  python
Python 3.5.6 |Anaconda, Inc.| (default, Aug 26 2018, 16:30:03)
[GCC 4.2.1 Compatible Clang 4.0.1 (tags/RELEASE_401/final)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>>


```

## 설치 후 테스트 
- https://tensorflowkorea.gitbooks.io/tensorflow-kr/content/g3doc/get_started/os_setup.html#test-the-tensorflow-installation
```bash
(tensorflow_py3.5)  jake.ko  ~  python
Python 3.5.6 |Anaconda, Inc.| (default, Aug 26 2018, 16:30:03)
[GCC 4.2.1 Compatible Clang 4.0.1 (tags/RELEASE_401/final)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
2018-12-14 17:49:06.272150: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
>>> print(sess.run(hello))
b'Hello, TensorFlow!'
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print(sess.run(a + b))
42
>>>

## 데모 모델을 포함해 텐서플로우의 모든 패키지는 파이썬 라이브러리로 설치되어 있습니다. 경로 찾기
(tensorflow_py3.5)  jake.ko  ~  python3 -c 'import os; import inspect; import tensorflow; print(os.path.dirname(inspect.getfile(tensorflow)))'
/anaconda2/envs/tensorflow_py3.5/lib/python3.5/site-packages/tensorflow

python3 /anaconda2/envs/tensorflow_py3.5/lib/python3.5/site-packages/tensorflow/examples/tutorials/mnist/mnist.py

##
(tensorflow_py3.5)  jake.ko  /usr/local/lib/python3.7/site-packages/tensorflow/models/image/mnist  pwd
/usr/local/lib/python3.7/site-packages/tensorflow/models/image/mnist
(tensorflow_py3.5)  jake.ko  /usr/local/lib/python3.7/site-packages/tensorflow/models/image/mnist  python3 /usr/local/lib/python3.7/site-packages/tensorflow/models/image/mnist/convolutional.py

```


## reference
- http://kamang-it.tistory.com/entry/Anaconda%EC%95%84%EB%82%98%EC%BD%98%EB%8B%A4-%EC%84%A4%EC%B9%98%ED%95%98%EB%8A%94%EB%B2%95%EA%B3%BC-%EC%82%AC%EC%9A%A9%EB%B2%95
- https://tensorflowkorea.gitbooks.io/tensorflow-kr/content/g3doc/get_started/os_setup.html
- https://github.com/tensorflow/tensorflow/issues/5478#issuecomment-281704288

tags:
