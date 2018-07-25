# TensorFlow Manual Installation
If you want (or you need) to install TF manually you might need to reproduce these basic steps

## Official Guide
Installation from sources from https://www.tensorflow.org/install/install_sources. This guide is awesome and well written.
With my latest CentOS release on an unfortunate CPU (no avx instructions...) these are requirements I have found.

### Environment
```
yum update
yum upgrade
yum install patch
yum install gcc-c++
yum install python34-numpy
yum install python-wheel
pip install wheel
```

### Bazel
[Bazel](https://www.bazel.build/) is required for building the whole software, unfortunately there's no such package inside CentOS
repository, so: if you are not able to `yum install bazel` (or whatever is called inside your repos) you might need to install it
with an alternative source, here's what I have done with a CentOS machine:
```
# EDIT /etc/yum.repos.d/vbatts-bazel-epel-7.repo
[vbatts-bazel]
name=Copr repo for bazel owned by vbatts
baseurl=https://copr-be.cloud.fedoraproject.org/results/vbatts/bazel/epel-7-$basearch/
type=rpm-md
skip_if_unavailable=True
gpgcheck=1
gpgkey=https://copr-be.cloud.fedoraproject.org/results/vbatts/bazel/pubkey.gpg
repo_gpgcheck=0
enabled=1
enabled_metadata=1
```
`yum update; yum upgrade` as usual and install bazel with `yum install bazel`


### configure, make, make install stuff
```
cd tensorflow
./configure
# This will take ages and tons of RAM.... take a nap...
bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package
./bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
pip install /tmp/tensorflow_pkg/tensorflow-x.x.x-cp34-cpxxm-linux_x86_64.whl
pip install --upgrade pip
```

### Installation Test
start your Python3 interpreter and try to issue these commands on console
```
# Python
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
```
It should print *something* and everything goes fine if your installation is correct, a core dump after `import` might be a symptom of
a wrong installation or incorrect compile flags
