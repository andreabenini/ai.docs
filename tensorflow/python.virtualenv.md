# Installation
Use virtualenv for everything. This avoids a mess with pip, tf libs and so on. These are required steps:
```
# Install virtualenv
emerge virtualenv # Or whatever you need with your package manager in order to use it

# python3 setup
virtualenv --system-site-packages -p python3 tensorflow

# Enter the environment, see commands below
source ./tensorflow/bin/activate

# Upgrade pip or install an up to date version
pip install --upgrade pip
# list of python installed packages
pip list

# Now install tensorflow
pip install --upgrade tensorflow     # Python 3, CPU
pip install --upgrade tensorflow-gpu # Python 3, GPU
# ... and wait for a while until it finishes

```
and you're set

# Environment
```
# Enter environment
source ~/tensorflow/bin/activate             # bash, sh, ksh, or zsh
> (tensorflow) /mnt/disk/home/ben $          # Entering virtualenv

# Exit environment
deactivate

# Upgrade tensorflow setup
pip3 install --upgrade tensorflow
pip3 install --upgrade tensorflow-gpu

# Remove a virtualenv installation
rm -r tensorflow                             # Directory where virtualenv was set

```
