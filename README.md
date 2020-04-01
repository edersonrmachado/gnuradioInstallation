### 0GNURadio Installation with PYBOMBS 
This GNURadio installation is prepared to work with UBUNTU 18.04 LTS version. 


#### 1. Install GNURadio dependences GNU Radio version 3.8.x with Python 3 support:
```
sudo apt install git cmake g++ libboost-all-dev libgmp-dev swig python3-numpy \
python3-mako python3-sphinx python3-lxml doxygen libfftw3-dev \
libsdl1.2-dev libgsl-dev libqwt-qt5-dev libqt5opengl5-dev python3-pyqt5 \
liblog4cpp5-dev libzmq3-dev python3-yaml python3-click python3-click-plugins \
python3-zmq python3-scipy 

```
#### 2. Install git, other dependences python-3 and pip3:
```
sudo apt install git
sudo apt-get update
sudo apt-get install libboost-all-dev libusb-1.0-0-dev python-mako doxygen python-docutils cmake build-essential
sudo apt install python3
sudo apt install python3-pip
```
#### 3. Install PYBOMBS: 
```
sudo pip3 install --force-reinstall  --no-cache-dir --upgrade git+https://github.com/gnuradio/pybombs.git
``` 
#### 4. Configure Pybombs:
```
pybombs recipes --no-cache  add-defaults
pybombs recipes -v  add-defaults
```
#### 5. Setting up a base folder to install GnuRadio:
```
cd ~
mkdir prefix  prefix/GNURADIO
```
#### 6. Change pybombs config file :
```
sudo gedit ~/.pybombs/config.yml 
``` 
Replace the code  by:
```
!!omap
- config:
    git-cache: ~/.pybombs/gitcache
    elevate_pre_args:
    - sudo
    - -H
    makewidth: 4
    packagers: apt,pymod,pip,pkgconfig,cmd
    default_prefix: ~/prefix/GNURADIO
- recipes:
    gr-etcetera: git+https://github.com/gnuradio/gr-etcetera.git
    gr-recipes: git+https://github.com/gnuradio/gr-recipes.git
```
Save this file (ctrl+s). 
#### 7. Then, specify the config file to be used in this installation:
```
pybombs auto-config -c  ~/.pybombs/config.yml
```
#### 8. And finally install:

```
pybombs -vv prefix init ~/prefix/GNURADIO -R gnuradio-default
```
It will take some hours...
#### 9. After a successful installation, adjust PATH config file (setup_env.sh) in order to prevent a reference error.   
```
cd ~/prefix/GNURADIO/
sudo gedit setup_env.sh
```
Add this path: "~/prefix/GNURADIO/lib/python3/dist-packages"  to PYTHONPATH:

```
export PYTHONPATH="~/prefix/GNURADIO/lib/python3/dist-packages:...blabla"
```
 As explained here by gareth8118 <https://github.com/gnuradio/pybombs/issues/553>
Save file
#### 10. And finally run GnuRadio:

```
source setup_env.sh 
gnuradio-companion 
```
