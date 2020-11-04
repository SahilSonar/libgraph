## Installing libgraph on Ubuntu 20.04 LTS

### Download libgraph from here:

```wget http://download.savannah.gnu.org/releases/libgraph/libgraph-1.0.2.tar.gz```

### Extract the libgraph:

```tar -xvf libgraph-1.0.2.tar.gz```

### From Ubuntu 18.04 guile-2.0 works but libesd0-dev is deprecated. For installing libesd0-dev you need to add repositories of xenial in sources.list.

``sudo nano /etc/apt/sources.list``

### Add these lines:

``deb http://us.archive.ubuntu.com/ubuntu/ xenial main universe `` </br>
``deb-src http://us.archive.ubuntu.com/ubuntu/ xenial main universe``

### Run ```sudo apt-get update``` Then install packages using:

 `` sudo apt-get install build-essential libsdl-image1.2 libsdl-image1.2-dev guile-2.0 guile-2.0-dev libsdl1.2debian libart-2.0-dev libaudiofile-dev libesd0-dev libdirectfb-dev libdirectfb-extra libfreetype6-dev libxext-dev x11proto-xext-dev libfreetype6 libaa1 libaa1-dev libslang2-dev libasound2 libasound2-dev g++ gcc make``

### The new libguile source is installed in /usr/include/guile/2.0/ copy pasta below lines 

``sudo mv /usr/include/guile/2.0/* /usr/include/ ``

### libgraph expects libguile.h to be in the standard include paths which it is not. The autoconf script should really find the correct locations (which I consider a build system bug) but it doesn't, so you need to add its include path to the preprocessor and linker flags. The standard approach would be:

``CPPFLAGS="$CPPFLAGS $(pkg-config --cflags-only-I guile-2.0)" \ 
  CFLAGS="$CFLAGS $(pkg-config --cflags-only-other guile-2.0)" \
  LDFLAGS="$LDFLAGS $(pkg-config --libs guile-2.0)" \ 
  ./configure
make ``

``sudo make install``

``sudo cp /usr/local/lib/libgraph.* /usr/lib``

### To compile it use: 

`` gcc test.c -o test ``

### To run:

 `` ./test ``

### Refrence: 
https://askubuntu.com/questions/942863/trying-to-install-libgraph </br>
https://askubuntu.com/questions/525051/how-do-i-use-graphics-h-in-ubuntu







