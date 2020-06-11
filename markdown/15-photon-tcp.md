---
---

```
cd code_idealab_ros/src
catkin_create_pkg photon_tcp std_msgs rospy roscpp
roscd photon_tcp/
mkdir msg
nano data.msg
```

paste in:

```
string ip_address
string data
```

follow instructions for adding a messsage

follow instructions for adding a script

1. Make project

    ```bash
    roscd thorlabs_linear_actuator/
    catkin_make
    ```