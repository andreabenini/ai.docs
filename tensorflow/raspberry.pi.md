# Method [1] Build from source (cross compiled with docker on PC)
Just follow Google instructions https://www.tensorflow.org/install/source_rpi .

Do not use other github resources for it, docker required on PC.


# Method [2] virtualenv, pip, piwheel
This is my suggested method, use virtualenv guide as reported in these markdown files for the PC Installation.
On Raspbian everything should be fine because it's a mainstream distro and it's fully supported from RPi foundation and
Google, if you're using a different distro (Arch, Gentoo, Suse) you need to slightly modify few steps.
Basic installation requirements (from your RPi distro):
- Basic Linear Algebra Subprograms [blas]
- Linear Algebra PACKage [lapack]
- ...or libatlas-dev as alternative, it depends on your distribution

Please remember to install:
- pip (upgrade to latest version)
- h5py
- numpy
- tensorflow
Do **not** use your package manager, use `pip` in a virtualenv instead

## Linux Arch Example
**NOTE:** Tensorflow compilation might tage _Ages_ so be prepared to that, you might also encounter problems with tmpfs
space. If you're using a stock /tmp dir with tmpfs filesystem you might run out of space quickly. To avoid it umount your
/tmp dir, create a new one and assign 1777 perms to it
```
umount /tmp
mv /tmp /tmp1
mkdir /tmp
chmod 1777 /tmp
```
Or resize your tmpfs accordingly, I have seen numpy and tensorflow compilation in trouble with a small tmpfs filesystem.
Get back to original state when you're done (something like: `mount -t tmpfs -o size=500M tmpfs /tmp`).


Modify `/etc/pip.conf` to include piwheels binary distributions (Ben Nuttall really rocks with it), create a new one if
non esistent and write these info into it.
```
[global]
extra-index-url=https://www.piwheels.org/simple
```
Now enter your virtualenv and install some stuff
```
# create python3 virtualenv setup
virtualenv --system-site-packages -p python3 tensorflow
# Enter the environment
source ./tensorflow/bin/activate
# Upgrade pip or install an up to date version
pip install --upgrade pip
# Now install tensorflow
pip install --upgrade tensorflow
```
Now have a nap until it's done, this method requires an huge amount of time because no cross compilation or host setup
is required, everything is done in your Pi.
numpy, h5py and tensorflow will be installed for you.


---
_drop me a note if you're having problems with that_
