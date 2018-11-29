# Installing ROS on TX-1 or TX-2

## Installing ROS (Kinetic for TX2)

Installing ROS on the Tegra devices is pretty straightforward, following the
instructions from the  official ROS Installer Guidelines.

Inside this repository you will find an executable shell script named
**ros-kinetic-install.sh**. This is a compilation of all the steps to install
ROS Kinetic on your TX1/TX2. This script will install the barebones version
of ROS-Kinetic. If you wish to install the full desktop version, comment
out the script that installs the **ros-base** version and uncomment the desired
version installer.

An additional note is in the initialization of **rosdep**. You may recieve a
warning requiring you  to fix your rosdep permission.

To do that, simply follow the instructions mentioned, i.e
```
sudo rosdep fix-permissions
rosdep update
source /opt/ros/ketic/setup.bash
```

At the end of the installer, you should be able to launch your **roscore** and
view your rosnode list successfully!

## Setting up CATKIN_TOOLS

I prefer to use *catkin_tools* and their package builder instead of *catkin_make*:

Setting it up is simple,
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu `lsb_release -sc` main" > /etc/apt/sources.list.d/ros-latest.list'
wget http://packages.ros.org/ros.key -O - | sudo apt-key add - 
sudo apt-get update
sudo apt-get install python-catkin-tools
```

### Creating a workspace
```
mkdir -p /path/to/workspace_ws/src
cd /path/to/workspace_ws
catkin config --init --extend /opt/ros/kinetic
```

### CMAKE Configuration
```
catkin config --cmake-args -DCMAKE_BUILD_TYPE=Debug
```

```
catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release
```
