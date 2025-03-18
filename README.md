# MIRAI
Autonomous exploration drone developed based on Fast_LIO and Ego-Planner algorithms
# Bill of Materials（BOM）
[NUC13VYKi5](https://www.asus.com.cn/displays-desktops/nucs/nuc-kits/nuc-13-pro-desk-edition-kit/techspec/)<br>
[MID360](https://www.livoxtech.com/cn/mid-360)<br>
[Ubuntu20.04.6](https://releases.ubuntu.com/focal/)
# Guidance for reference
_PX4_:<br>
https://docs.px4.io/main/en/<br>
https://docs.px4.io/main/en/ros/mavros_installation.html<br>
_ROS_:<br>
https://wiki.ros.org/ROS<br>
https://wiki.ros.org/ROS/Installation<br>
https://wiki.ros.org/noetic/Installation/Ubuntu<br>
_MavROS_<br>
https://wiki.ros.org/mavros<br>
_QGC(QGroundControl)_<br>
https://qgroundcontrol.com/<br>
https://github.com/ZJU-FAST-Lab/ego-planner<br>
https://github.com/hku-mars/FAST_LIO<br>
https://github.com/Livox-SDK/livox_ros_driver2<br>

```shell
$sudo dpkg -i .deb
$sudo apt install .deb
$sudo apt -f install
```

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
```
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

