---
title: Installation of Opencv, numpy, scipy inside a virtualenv
layout: post
author: manu
categories: jekyll testing
---

Useful for python server side deployments that need computer vision.

I did this for a ubuntu 13.04 server. This should work for 12.10 without much of a problem.

### Activate the virtualenv

{% highlight bash %}
source bin/activate 
# or
workon <environment_name>
{% endhighlight %}

For numpy and scipy it’s fairly simple

{% highlight bash %}
pip install numpy scipy
{% endhighlight %}

You can go by two approaches. One is to install opencv globally in your system and then moving those libraries to your virtualenv. This approach has some shortcomings. The globally installed opencv might have been compiled for a different version of python. It gets difficult during deployment to point to the right environment.

### Copy globally installed opencv into your virtualenv

Use this incase you want to copy your system installed opencv over to your virtualenv. In the virtualenv you make for your project, do the following.


Copy cv.* (from OpenCV-2.2.0/lib directory) to the virtualenv site-packages

{% highlight bash %}
cp /usr/lib/pymodules/python2.7/cv* 
$VIRTUAL_ENV/lib/python2.7/site-packages/
{% endhighlight %}

Again, I have seen this approach used only by an intern. I can’t vouch for it’s reliability.

The second approach mitigates some of those problems. Thanks to some helpful people on the web, I could figure out how to install OpenCV inside a virtualenv without touching the global python

### Dependencies
For opencv, there are system dependencies which can be installed like so,

{% highlight bash %}
sudo apt-get install cmake libgtk2.0-dev pkg-config libavcodec-
dev libavformat-devlibswscale-dev libamd2.2.0 libblas3gf libc6
libgcc1 libgfortran3 liblapack3gf libumfpack5.4.0 libstdc++6 
build-essential gfortran libatlas-dev libatlas3-base libblas-dev
liblapack-dev libjpeg-dev libpng-dev libtiff-devlibjasper-dev
{% endhighlight %}

## Download opencv, build it and install it

### Downloading

Navigate to a folder to download opencv and download it
{% highlight bash %}
cd opencv-2.4.5/
mkdir release
cd release

# notice that in the command below, 
# -D INSTALL_PYTHON_EXAMPLES=ON 
# is optional.

cmake -D MAKE_BUILD_TYPE=RELEASE -D 
CMAKE_INSTALL_PREFIX=$VIRTUAL_ENV/local/ -D 
PYTHON_EXECUTABLE=$VIRTUAL_ENV/bin/python -D 
PYTHON_PACKAGES_PATH=$VIRTUAL_ENV/lib/python2.7/site-packages -D
INSTALL_PYTHON_EXAMPLES=ON ..
{% endhighlight %}

### Installation

{% highlight bash %}
make -j8
make install
{% endhighlight %}

### Testing if everything went right

Get into python shell and try the following commands
{% highlight bash %}
# enter python shell
# make sure your environment is activated
python
{% endhighlight %}

now inside the shell, try the following imports

{% highlight pycon %}
import cv
import cv2
import numpy
import scipy
{% endhighlight %}

these imports shouldn't throw any error

Later, you might run into a decoder error. As a precaution, reinstall Pillow

{% highlight python %}
pip freeze | grep Pil # to find the Pillow version we're using
pip -I install Pillow==2.0.0 # or whichever version you find from the step above
{% endhighlight %}









