Note: This tutorial goes through how to do it from scratch.  the libnifalcon repository is now forked [here](https://github.com/idealabasu/libnifalcon).  Furthermore, the [idealab_ros_tools](https://github.com/idealabasu/code_idealab_ros) repository now has the current working copy of the ros_falcon package in it.  the original ros_falcon package has been forked and is now [here ](https://github.com/idealabasu/ros_falcon)

1. add falcon to virtualbox ('Future Technology Devices International, Ltd FALCON HAPTIC [0400]')

1. open up virtualbox and check to see if it is found 

```bash
dmesg | grep FALCON
```	

1. install libusb

```bash
sudo apt install libusb
```

1. clone repository

```bash
cd ~/
git clone https://github.com/libnifalcon/libnifalcon.git
cd ~/libnifalcon
```

1. follow instructions

```bash
cd ~/libnifalcon
mkdir build
cd build
cmake -G "Unix Makefiles" ..
make
sudo make install
```


1. add device udev file

	1. get [this modified file](https://drive.google.com/open?id=1y2G6Skq7Whxg6oW7PQahXXxbPsS8SYJ1&authuser=daukes@asu.edu&usp=drive_fs)
	
	Note: you can now get the file within the idealab_ros_tools repository

```
#the default one doesn't seem to work
#sudo cp ~/libnifalcon/linux/40-novint-falcon-udev.rules /etc/udef/rules.d/
sudo cp ~/code_idealab_ros/src/ros_falcon/udev/99-udev-novint.rules /etc/udef/rules.d/
sudo chmod 644 99-udev-novint.rules
sudo udevadm control --reload-rules && udevadm trigger
```

1. run ```findfalcons``` several times until you see it


1. add joy package
```bash
sudo apt install ros-melodic-joy
```

1 clone ros repository

```bash
cd ~/
git clone https://github.com/idealabasu/ros_falcon.git
roscd ros_falcon
# cd nodes
#chmod +x joy2cmd_vel.py
rosrun ros_falcon driver
```

in a new window:

```
roscore
```

in a new window:

```
rostopic echo /falconPos
```