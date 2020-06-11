## ROS Instalation Summary

from [here](https://wiki.ros.org/melodic/Installation/Ubuntu)

1. Run this code:  
Note: Using ```ros-melodic-desktop-full```

    ```bash
    #Setup your computer to accept software from packages.ros.org.
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

    #Set up your keys
    sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

    sudo apt update
    sudo apt install ros-melodic-desktop-full
    #sudo apt install ros-melodic-desktop
    #sudo apt install ros-melodic-ros-base

    #To find available packages, use:
    #apt search ros-melodic

    #It's convenient if the ROS environment variables are automatically added to your bash session every time a new shell is launched:
    echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
    echo "export EDITOR='nano -w'" >> ~/.bashrc #from https://wiki.ros.org/ROS/Tutorials/UsingRosEd
    source ~/.bashrc


    #To install tools and other dependencies for building ROS packages, run:
    sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
    #not sure if you need to do the next line.
    #sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
    #sudo apt install python-rosdep

    sudo rosdep init
    rosdep update
    ```
1. Install catkin tools

    ```
    sudo apt install -y catkin-tools
    sudo apt install -y python3-pip python3-yaml
    sudo pip3 install rospkg catkin_pkg empy
    
    ```

1. Take a Snapshot

## Installing and Configuring Your ROS Environment

from [here](https://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment)

```bash
# this has been added to bashrc so is not necessary
source /opt/ros/melodic/setup.bash

#Let's create and build a catkin workspace:

mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
#for Python 3 users, the first catkin_make command in a clean catkin workspace must be:
catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3
# for python2.x
#catkin_make

#source your new setup.*sh file:
source devel/setup.bash

#make sure ROS_PACKAGE_PATH environment variable includes the directory you're in.
echo $ROS_PACKAGE_PATH
```

## Ros Filesystem (optional)

From [here](https://wiki.ros.org/ROS/Tutorials/NavigatingTheFilesystem)

```bash
#sudo apt-get install ros-<distro>-ros-tutorials
sudo apt-get install ros-melodic-ros-tutorials
#rospack find [package_name]
rospack find roscpp
#roscd [locationname[/subdir]]
roscd roscpp
#print the working directory using the Unix command
pwd
#To see what is in your ROS_PACKAGE_PATH, type:
echo $ROS_PACKAGE_PATH

#roscd can also move to a subdirectory of a package or stack.  Try:
roscd roscpp/cmake
pwd

#roscd log will take you to the folder where ROS stores log files. Note that if you have not run any ROS programs yet, this will yield an error saying that it does not yet exist.
#If you have run some ROS program before, try:
roscd log

#rosls is part of the rosbash suite. It allows you to ls directly in a package by name rather than by absolute path.
#rosls [locationname[/subdir]]
rosls roscpp_tutorials
```