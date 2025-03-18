# MIRAI
Autonomous exploration drone developed based on Fast_LIO and Ego-Planner algorithms
# Bill of Materials（BOM）
* Hardware<br>
[NUC13VYKi5](https://www.asus.com.cn/displays-desktops/nucs/nuc-kits/nuc-13-pro-desk-edition-kit/techspec/)<br>
[MID360](https://www.livoxtech.com/cn/mid-360)<br>
AP-H743V2
* Software<br>
[Ubuntu20.04.6](https://releases.ubuntu.com/focal/)<br>
[ROS_noetic](https://wiki.ros.org/noetic)<br>
[Nuttx](https://nuttx.apache.org/)<br>
# Guidance for reference
_ROS_:<br>
https://wiki.ros.org/ROS<br>
https://wiki.ros.org/ROS/Installation<br>
https://wiki.ros.org/noetic/Installation/Ubuntu<br>
_MavROS_<br>
https://wiki.ros.org/mavros<br>
_PX4_:<br>
https://docs.px4.io/main/en/<br>
https://docs.px4.io/main/en/ros/mavros_installation.html<br>
_QGC(QGroundControl)_<br>
https://qgroundcontrol.com/<br>
https://github.com/ZJU-FAST-Lab/ego-planner<br>
https://github.com/hku-mars/FAST_LIO<br>
https://github.com/Livox-SDK/livox_ros_driver2<br>

Common software installation commands：
```shell
sudo dpkg -i .deb
sudo apt install .deb
sudo apt -f install
```
Network status and network hardware information query：
```
ifconfig #Check the basic configuration information of the network card, including the name of the network card
sudo lshw -class network #View the local network card information
lspci -v #View the network card information of the PCI device
sudo vi /etc/network/interfaces #Open the network card configuration file to view
```
Download the offline compilation and installation from the following link：<br>
[linux-firmware](https://web.git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/)<br>
[backport-iwlwifi](https://web.git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git/)<br>
```
tar -zxvf XXX.tar.gz
```
Solve network card driver problems online：
```shell
sudo apt update
sudo apt-get upgrade
sudo apt-get install -y git
sudo apt-get install -y build-essential
sudo apt-get install make
sudo apt install flex bison
#Download linux-firmware
git clone git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
cd linux-firmware
sudo cp iwlwifi-* /lib/firmware/
cd ..
```
```
git clone -b release/core76 https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git
cd backport-iwlwifi
sudo make defconfig-iwlwifi-public
sudo make -j4
sudo make install
```
```
reboot
```

# ROS One-line Installation
Single-line installation The following line of command will install the latest ROS Noetic Ninjemys on Ubuntu Focal 20.04. Copy & Paste this line of command into the Ubuntu terminal.
TwoLineInstall


```
wget -c https://raw.githubusercontent.com/qboticslabs/ros_install_noetic/master/ros_install_noetic.sh && chmod +x ./ros_install_noetic.sh && ./ros_install_noetic.sh
```
The following line of command will uninstall ROS Noetic Ninjemys
```
wget -c https://raw.githubusercontent.com/qboticslabs/ros_install_noetic/master/ros_uninstall_noetic.sh && chmod +x ./ros_uninstall_noetic.sh && ./ros_uninstall_noetic.sh
```
Test Program
```shell
roscore #Open rosmaster
rosrun turtlesim turtlesim_node #Open the little turtle visualization interface
rosrun turtlesim turtle_teleop_key #Open the turtle keyboard control node
rqt_graph
```
# Livox-SDK2
Instruction for Ubuntu 20.04
Dependencies:
* [CMake 3.0.0+](https://cmake.org/)
* gcc 4.8.1+
Install the **CMake** using apt:
```shell
$ sudo apt install cmake
```
Compile and install the Livox-SDK2:

```shell
$ git clone https://github.com/Livox-SDK/Livox-SDK2.git
$ cd ./Livox-SDK2/
$ mkdir build
$ cd build
$ cmake .. && make -j
$ sudo make install
```

**Note :**  
The generated shared library and static library are installed to the directory of "/usr/local/lib". The header files are installed to the directory of "/usr/local/include".

Tips: Remove Livox SDK2:

```shell
$ sudo rm -rf /usr/local/lib/liblivox_lidar_sdk_*
$ sudo rm -rf /usr/local/include/livox_lidar_*
```
fast_lio/src/livox_ros_driver2/config/MID360_config.json
```
{
  "lidar_summary_info" : {
    "lidar_type": 8
  },
  "MID360": {
    "lidar_net_info" : {
      "cmd_data_port": 56100,
      "push_msg_port": 56200,
      "point_data_port": 56300,
      "imu_data_port": 56400,
      "log_data_port": 56500
    },
    "host_net_info" : {
      "cmd_data_ip" : "192.168.1.5",  	# <-This is consistent with the modified computer IP
      "cmd_data_port": 56101,
      "push_msg_ip": "192.168.1.5",    	# <-This is consistent with the modified computer IP
      "push_msg_port": 56201,
      "point_data_ip": "192.168.1.5",  	# <-This is consistent with the modified computer IP
      "point_data_port": 56301,
      "imu_data_ip" : "192.168.1.5",  	# <-This is consistent with the modified computer IP
      "imu_data_port": 56401,
      "log_data_ip" : "",
      "log_data_port": 56501
    }
  },
  "lidar_configs" : [
    {
      "ip" : "192.168.1.123",		  	     # <-Here is the IP address of Livox mid360
      "pcl_data_type" : 1,
      "pattern_mode" : 0,
      "extrinsic_parameter" : {
        "roll": 0.0,
        "pitch": 0.0,
        "yaw": 0.0,
        "x": 0,
        "y": 0,
        "z": 0
      }
    }
  ]
}

```
Terminal startup
```
roslaunch livox_ros_driver2 msg_MID360.launch
```
New terminal（Ctrl+Alt+T）
```
roslaunch fast_lio mapping_mid360.launch
```


# Quick Start within 3 Minutes 
Compiling tests passed on ubuntu **16.04, 18.04 and 20.04** with ros installed.
You can just execute the following commands one by one.
```
sudo apt-get install libarmadillo-dev
git clone https://github.com/ZJU-FAST-Lab/ego-planner.git
cd ego-planner
catkin_make
source devel/setup.bash
roslaunch ego_planner simple_run.launch
```
If your network to github is slow, We recommend you to try the gitee repository [https://gitee.com/iszhouxin/ego-planner](https://gitee.com/iszhouxin/ego-planner). They synchronize automatically.




If you find this work useful or interesting, please kindly give us a star :star:, thanks!:grinning:



