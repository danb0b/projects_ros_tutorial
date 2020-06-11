## Nomenclature

If you are installing a linux virtual machine on your windows computer, your windows computer is called the "host", and the linux virtual machine is called the "guest"

## Host Computer installation stuff

You will need some packages installed on the host side to communicate with your guest(virtual) machine

1. from command prompt:

    ```
    pip install service_identity roslibpy
    ```
1. Install [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) for ssh acess

## Creating the Guest OS  -- Pre-ROS steps 

1. Create Virtual Machine
    * 4Gb Ram
    * 50Gb HD, flexible size option
    * 1-2 cpus
    * load ubuntu 18.04 iso
1. Install Ubuntu
    * minimum install
    * no 3rd party
    * no downloads
    * username: idealab
    * pw: idealab
    * sign in automatically
1. snapshot
1. install guest additions
    1. Run this

        ```bash
        sudo apt install -y virtualbox-guest-utils virtualbox-guest-dkms
        ```
    
    1. then install the virtualbox guest additions cd from the guest os window and select run when the button pops up.
    1. let it run
    1. eject the cd
    1. Restart guest
1. Install other packages

    ```bash
    #update repository
    sudo apt update

    #visual package manager
    sudo apt install -y synaptic

    #ssh access
    sudo apt install -y openssh-server

    #python editor
    sudo apt install -y spyder3

    #ifconfig
    sudo apt install net-tools

    #misc
    sudo apt install -y curl

	#python packages
	sudo apt install -y python3-serial python3-pip
    ```

1. snapshot



follow directions at <https://wiki.ros.org/melodic/Installation/Ubuntu>

## Guest Network Setup

1. change virtualbox network settings to "bridged adapter" mode
1. find the ip address of ethernet port

    ```bash
    #sudo apt install net-tools
    ifconfig -v
    ```

1. this will return information about each networking device, that looks like this:

    ```
    enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.0.17  netmask 255.255.255.0  broadcast 192.168.0.255
            inet6 2600:8800:2281:3600:a6d7:41a9:9d6b:e48b  prefixlen 64  scopeid 0x0<global>
            inet6 fe80::7804:5434:c83:a827  prefixlen 64  scopeid 0x20<link>
            inet6 2600:8800:2281:3600:588c:62a0:442a:d6ce  prefixlen 64  scopeid 0x0<global>
            ether 08:00:27:00:80:00  txqueuelen 1000  (Ethernet)
            RX packets 47127  bytes 47300474 (47.3 MB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 13563  bytes 1385399 (1.3 MB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

    lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 1000  (Local Loopback)
            RX packets 117914  bytes 20197993 (20.1 MB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 117914  bytes 20197993 (20.1 MB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ```
    
1. The value you want is the "inet" value under, in this case, enp0s3, or 192.168.0.17 in our case.  Remember this value, this is how you will communicate with your virtual pc
