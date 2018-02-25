### install tensorflow with anaconda
configuration: ubuntu 14.04, CUDA8.0, CUDNN v5, python2.7, anaconda2
[tensorflow website1](https://www.tensorflow.org/install/install_linux)
[tensorflow website2](https://www.tensorflow.org/versions/r0.12/get_started/os_setup#anaconda_installation)

* Create a conda environment named tensorflow to run a version of Python by invoking the following command:
```
$ conda create -n tensorflow pip python=2.7
```
* Activate the conda environment by issuing the following command:
```
$ source activate tensorflow
 (tensorflow)$  # Your prompt should change 
```
* Issue a command of the following format to install TensorFlow inside your conda environment:
```
# Ubuntu/Linux 64-bit, GPU enabled, Python 2.7
# Requires CUDA toolkit 8.0 and CuDNN v5. For other versions, see "Installing from sources" below.
(tensorflow)$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-0.12.1-cp27-none-linux_x86_64.whl
(tensorflow)$ pip install --ignore-installed --upgrade $TF_BINARY_URL
```

* test installation
```
$ python
...
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))
Hello, TensorFlow!
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print(sess.run(a + b))
42
>>>
```

* usage
```
$ source activate tensorflow
(tensorflow)$  # Your prompt should change.
# Run Python programs that use TensorFlow.
...
# When you are done using TensorFlow, deactivate the environment.
(tensorflow)$ source deactivate
```
