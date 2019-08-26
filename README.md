# Deep Learning Workstations

## Why investing my own deep learning workstation?
The nature of deep learning determines that researchers and practioners spend lots of their time on experimentation and iteration. Cloud computing provides fast, secure, and scalable solutions for companies. However, for deep learning enthusiasts, for long-term, owing a deep learning workstation is more cost-efficient than cloud computing solutions. 

## Where to buy workstations?
A year ago, I spent about 4,500 dollars to purchase my own deep learning workstation from the following website and I have no regrets. I used the following steps to set up my machine. 

https://mitxpc.com/collections/deep-learning/workstations

## how to set up your workstation?

### Ubuntu

Version: 18.04.2
https://help.ubuntu.com/lts/installation-guide/index.html

### Network with Static IPs

```bash
$ sudo apt update
$ sudo apt install openssh-server
$ sudo vim /etc/ssh/sshd_config
$ cat /etc/netplan/01-network-manager-all.yaml

# Allow NetworkManager manage all devices on this system
network:
  version: 2
  # renderer: NetworkManager
  renderer: networkd
  ethernets:
    enp0s31f6:
      dhcp4: no
      dhcp6: no
      addresses: [50.208.213.27/29, ]
      gateway4:  50.208.213.30
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]

$ sudo netplan apply
```

### Deb

#### common packages

```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install vim mc tree tmux htop nvidia-utils-390
$ sudo apt install kile texlive
$ sudo apt autoremove
```

```bash
$ sudo apt install xclip
$ sudo dpkg -i common-setup_1.0.16_all.deb
# After installation, empty the file ${User}/.bashrc.
```

#### Python

```bash
$ sudo apt update
$ sudo apt install python3-pip python3-venv
$ sudo apt install pkg-config graphviz opencv
$ sudo pip3 install altair vega_datasets jupyterlab numpy scipy
$ sudo pip3 install graphviz hypothesis ipython jupyter matplotlib
$ sudo pip3 install notebook pydot python-nvd3 pyyaml requests scikit-image
```

#### Docker

```bash
$ sudo apt update
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
$ sudo apt update
$ sudo apt install docker-ce
```

### Add Users

```bash
$ sudo adduser --system --home=/home/ginger --shell=/bin/bash ginger
$ sudo usermod -aG sudo,docker ginger
```

## Deep Learning Frameworks

### CUDA

```bash
$ sudo apt install cuda-repo-ubuntu1804-10-1-local-10.1.168-418.67_1.0-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-10-1-local-10.1.168-418.67/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install cuda
```

Reboot and check if the driver is applied:

```bash
$ nvidia-smi
```

### cuDNN

Download cuDNN v7.5.0 (Feb 25, 2019), for CUDA 10.1.

```bash
$ sudo apt install libcudnn7_7.5.0.56-1+cuda10.1_amd64.deb
$ sudo apt install libcudnn7-dev_7.5.0.56-1+cuda10.1_amd64.deb
```

### MXNet/Gluon

```bash
$ sudo pip3 install mxnet-cu101
```

### Tensorflow/Keras/PyTorch/Caffe2

#### Install in venv:

```bash
$ mkdir my_tensorflow
$ cd my_tensorflow
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $ pip install --upgrade pip
(venv) $ pip install --upgrade tensorflow-gpu
(venv) $ pip install --upgrade keras
(venv) $ pip install --upgrade https://download.pytorch.org/whl/cu100/torch-1.1.0-cp36-cp36m-linux_x86_64.whl
(venv) $ pip install --upgrade https://download.pytorch.org/whl/cu100/torchvision-0.3.0-cp36-cp36m-linux_x86_64.whl
(venv) $ pip install --upgrade future
(venv) $ pip install --upgrade caffe2
(venv) $ python -c 'import tensorflow as tf; print(tf.__version__)'
(venv) $ deactivate
```

#### Install Globally

```bash
$ pip3 install tensorflow-gpu
$ pip3 install keras
$ pip3 install https://download.pytorch.org/whl/cu100/torch-1.1.0-cp36-cp36m-linux_x86_64.whl
$ pip3 install https://download.pytorch.org/whl/cu100/torchvision-0.3.0-cp36-cp36m-linux_x86_64.whl
$ sudo pip3 install future
$ sudo pip3 install caffe2
```

#### Verify Tensorflow-GPU Works

```python
from tensorflow.python.client import device_lib
device_lib.list_local_devices()
```

#### Verify PyTorch Works

```python
import torch
torch.cuda.is_available()
# True
torch.cuda.get_device_name(0)
# 'GeForce GTX 1080 Ti'
torch.cuda.device_count()
```

#### Verify Caffe2 Works

```python
from caffe2.python import workspace, model_helper
```
