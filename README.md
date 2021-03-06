RobotPy RoboRIO Packages
========================

This repository contains the build files used to build the RobotPy .ipk
packages hosted at https://www.tortall.net/~robotpy/feeds/2017/. The current
list of published packages can be found at that URL.

Installing a package (online)
-----------------------------

Create a `.conf` file in `/etc/opkg` (e.g. `/etc/opkg/robotpy.conf`)
containing the following line:

    src/gz robotpy https://www.tortall.net/~robotpy/feeds/2017

Then run `opkg update`. After you setup the opkg feed, you can run:

    opkg install PACKAGENAME

Installing a package (offline)
------------------------------

You can use the [RobotPy Installer Script](https://github.com/robotpy/robotpy-wpilib/blob/master/installer/installer.py)
to do offline opkg installs. First, download the package:

    python3 installer.py download-opkg PACKAGENAME
    
Then, connect to the network with the RoboRIO, and install it:

    python3 installer.py install-opkg PACKAGENAME


Building these packages yourself
================================

Many of these packages are built directly on a roboRIO. Compiling them can
eat up most of your RoboRIO's disk space, so you'll probably want to reimage it
before using the RoboRIO in a competition.

Go into a directory and do this:

    make ROBORIO=roborio-XXXX-frc.local all

Build Notes
-----------

* You will almost certainly want to setup passwordless login using an SSH key,
  as the compile process uses SSH to login to the roborio multiple times.

* Most of these packages can be compiled on a virtual machine, and
  the virtual machine won't run out of disk space or RAM quite so easily. See
  the [roborio-vm](https://github.com/robotpy/roborio-vm) repository for more
  details.

* Some packages use a lot of RAM, and your best bet is to use a swap device to
  allow it to complete. A USB memory stick works great for this.
  * On a linux host use `cfdisk` to partition your stick
  * Use `mkswap` to initialize the space.
  * Mount it on the roborio by using `swapon`

When adding new packages:

* Some packages have deeply recursive build functionality, if you have a weird
  segfault that occurs it might be because the process ran out of stack space 
  (the default on the RoboRIO is 256k, whereas modern linux default to a few MB).
  In your build steps, you can set the stack size by executing `ulimit -s 2048`
