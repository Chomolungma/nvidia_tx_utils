# Install Basic Tools and Packages

## Basic Tools

```
sudo apt-get update
sudo apt-get install -y htop
sudo apt-get install -y tmux
sudo apt-get install -y vim
sudo apt-get install -y python3-pip
sudo apt-get install -y openssh-server
sudo apt-get install -y openssh-client
sudo apt-get install -y git
sudo apt-get install -y gfortran
sudo apt-get install -y protobuf-compiler
sudo apt-get install -y libprotoc-dev
sudo apt-get install python3-imaging
```

### Python related libraries
```
sudo pip3 install Cython
sudo pip3 install scikit-image
sudo pip3 install numpy
sudo pip3 install onnx
sudo pip3 install rosdep
sudo pip3 install rosinstall_generator
sudo pip3 install wstool
sudo pip3 install rosinstall
```

## Change *HOSTNAME*

Replace *tegra-ubuntu* or whatever existing hostname with your desired hostname:
```
sudo vim /etc/hostname
```
also in the following file:
```
sudo vim /etc/hosts
```



