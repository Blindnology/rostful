[![Build Status](https://travis-ci.org/asmodehn/rostful.svg?branch=indigo-devel)](https://travis-ci.org/asmodehn/rostful)

Overview
========

ROStful - A REST API for ROS.

Rostful is intended to be the outside layer of a ros system,
communicating with the outside world via HTTP,
and exposing a REST API to use the robot services, or introspect robot topics.
As such this should be launched either : 
 - as a python code with the de facto python standard behaviors ( venv, pip requirements, etc. ),

``` python -m rostful flask ```

 - as a ros package, with the de facto ros standard behaviors.

``` roslaunch rostful rostful.launch ```

so that users from both world can use it efficiently.

What will not be in Rostful
===========================
 - Security related stuff ( Authentication/Authorization ) implementation.
 We will not provide here any Authentication/Authorization mechanisms without ROS providing one first.
 And even after that, the implications of such an implementation would probably fit better in another specific microservice, that we would rely on in rostful.

PYTHON VIRTUALENV SETUP
=======================

How to setup your python virtual environment on Ubuntu (tested on Trusty
14.04)
 - Install and Setup virtualenvwrapper if needed
``` sudo apt-get install virtualenvwrapper echo "source /etc/bash_completion.d/virtualenvwrapper" >> ~/.bashrc ```

 - Create your virtual environment for your project
``` mkvirtualenv myproject --no-site-packages workon myproject ```

 - Populate it to use rostful. The catkin dependency is temporarily needed
to be able to use the setup.py currently provided in rostful.
``` pip install catkin-pkg rostful ```

Installation
============
`pip install pip install pyros-interfaces-ros pytest-timeout==1.4.2 pyros==0.4.2 flask`

`sudo apt install ros-melodic-pyros-utils`

**Note:** The `pytest-timeout` version >= `2.0.0` does not support `python 2.x`.

Download dependencies

`git submodule init`

`git submodule update`

ROS service can take time, so we need to update Web server timeouts.

send timeout to 1 minute

```sudo sed -i 's/send_timeout=1000/send_timeout=60000/g' /home/ubuntu/.local/lib/python2.7/site-packages/pyzmp/service.py```

receive timeout to 5 minutes

```sudo sed -i 's/recv_timeout=5000/recv_timeout=300000/g' /home/ubuntu/.local/lib/python2.7/site-packages/pyzmp/service.py```

