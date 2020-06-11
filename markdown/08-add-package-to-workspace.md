---
---

1. Clone the idealab repository

    ```bash
    git clone https://github.com/idealabasu/code_idealab_ros.git
    ```
1. Create a new workspace (upon creation of new repository)

    ```bash
    cd ~/code_idealab_ros/src/
    catkin_create_pkg falcon std_msgs rospy roscpp
    cd ~/code_idealab_ros/
    catkin_make
    ```
1. 

```bash
cd ~/code_idealab_ros/src/falcon
nano package.xml
```

1. edit 

1. paste in the following

```
<build_depend>message_generation</build_depend>
<exec_depend>message_runtime</exec_depend>
```

1. save then close

1. create messages

```bash
mkdir msg
cd msg
nano Message1.msg
```

1. add message support to CMakeLists (see other tutorial)
1. Make project

    ```bash
    cd ~/code_idealab_ros/
    catkin_make
    ```
