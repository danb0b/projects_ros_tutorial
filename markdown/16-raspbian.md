Installing ROS on a Raspberry Pi 4 is difficult because, though the ubuntu images seem good to go, I experienced unknown problems setting up a headless install of ubuntu 18.  Ubuntu 20.04 worked eventually, but initial startup took over 5 minutes for the device to show up on my network.  Plus I was interested in installing ros melodic, which is built for ubuntu 18.  So here are the steps I used:

1. Download the Raspberry Pi Imager
    https://www.raspberrypi.org/downloads/

alternate: win32diskimager
alternate: https://www.balena.io/etcher/

1. Download an Image: I used the lite version and then added packages as needed
https://www.raspberrypi.org/downloads/raspbian/

1. Install raspbian using the instructions for a headless install located here:

https://www.raspberrypi.org/documentation/configuration/wireless/headless.md

alternate instructions: https://hackernoon.com/raspberry-pi-headless-install-462ccabd75d0


1. Make sure you follow the instructions below for  setting up wireless & ssh
https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md
https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md

International codes
https://en.wikipedia.org/wiki/ISO_3166-1

https://thepihut.com/blogs/raspberry-pi-tutorials/remotely-accessing-the-raspberry-pi-via-rdp-gui-mode

http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Melodic%20on%20the%20Raspberry%20Pi

1. Find your Pi on your network (in linux):

```
sudo apt install -y net-tools nmap
arp -na
nmap -sn 10.0.0.*
```

1. log on using putty

1. Define Static IP Address: https://www.ionos.com/digitalguide/server/configuration/provide-raspberry-pi-with-a-static-ip-address/

sudo nano /etc/dhcpcd.conf

uncomment out lines for static ip/subnet and router.

sudo reboot

alternate (I didn't use): https://thepihut.com/blogs/raspberry-pi-tutorials/tutorial-how-to-give-your-raspberry-pi-a-static-ip-address

https://www.raspberrypi.org/forums/viewtopic.php?t=133691

install xrdp:

https://thepihut.com/blogs/raspberry-pi-tutorials/remotely-accessing-the-raspberry-pi-via-rdp-gui-mode

install gedit

sudo apt install gedit

Install ROS:

http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Melodic%20on%20the%20Raspberry%20Pi

alternate(didn't use): https://www.seeedstudio.com/blog/2019/08/01/installing-ros-melodic-on-raspberry-pi-4-and-rplidar-a1m8/

https://projects.raspberrypi.org/en/projects/getting-started-with-picamera
sudo apt install gpicview vlc thonny
pip3 install picamera

change password

```
passwd
```

1. install opencv

https://www.pyimagesearch.com/2019/09/16/install-opencv-4-on-raspberry-pi-4-and-raspbian-buster/

don't use virtualenv...space reasons.
use sudo pip3 install instead of pip install

after installing picamera there is a warning.  use the next lines to fix

echo "export PATH=\$PATH:/home/pi/.local/bin" >> ~/.bashrc
source ~/.bashrc

sudo apt install -y libilmbase-dev libopenexr-dev libgstreamer1.0-dev

1. clone raspicam node

git clone https://github.com/idealabasu/raspicam_node.gits

not sure this is needed:
```
sudo apt install python3-catkin-pkg
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
sudo apt-get install python3-empy
```

1. update ros install with joystick and compressed image transport packages, following instructions here:

http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Melodic%20on%20the%20Raspberry%20Pi#Maintaining_a_Source_Checkout

and using 

```
rosinstall_generator ros_comm joystick_drivers compressed_image_transport camera_info_manager dynamic_reconfigure diagnostic_updater cv_bridge --rosdistro melodic --deps --wet-only --tar > melodic-custom_ros.rosinstall
```

1. add idealab ros workspace: (see other tutorial)

1. checkout rpi4 branch

1. cloned and copied raspicam_node into code_idealab_ros/src

1. Make projects

```
catkin_make
```



1. optional: change ros master uri to remote

#echo "export ROS_MASTER_URI=10.0.0.201:11311" >> .bashrc


echo "export MY_MASTER_IP=10.0.0.201" >> .bashrc
echo "export MY_IP=10.0.0.200" >> .bashrc
echo "export ROS_MASTER_URI=http://\$MY_MASTER_IP:11311" >> .bashrc
echo "export ROS_IP=\$MY_IP" >> .bashrc

source .bashrc

1. Run Roslaunchp

```
#roslaunch raspicam_node camerav2_1280x720.launch
#roslaunch raspicam_node camerav2_410x308_30fps.launch
roslaunch raspicam_node dan_cam1.launch

```

(modified from: https://www.theconstructsim.com/publish-image-stream-ros-kinetic-raspberry-pi/)


on the host:

rosrun rqt_image_view rqt_image_view