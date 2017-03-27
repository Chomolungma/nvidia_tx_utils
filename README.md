# NVIDIA - TX1 and TX2
Repository of all NVIDIA TX-1/TX-2 related code and usage instructions. 

## Initial Set-up
STEP 1: When you boot up the Jetson TX1/TX2 for the first time a terminal window will appear. To use the Ubuntu via the GUI, install the Nvidia Linux drive <br/>
From the home directory (use username: **ubuntu** and password: **ubuntu**)<br/>
for the NVIDIA TX-2 : username : **nvidia** and password: **nvidia**<br/>

>$ cd NVIDIA-INSTALLER <br/>

>$ sudo ./installer.sh <br/>

STEP 2: After the installation completes reboot the device,<br/>
>$ sudo reboot <br/>

STEP 3: You should now be able to log into the Ubuntu GUI

***

## Installing JetPack 
Link - https://developer.nvidia.com/embedded/jetpack<br/>
STEP 1: Download **JetPack** on the Host Machine by joining *Embedded System Developer* programme on NVIDIA page<br/>
The latest verson at the time of writing was *JetPack-L4T-2.3.1-linux-x64.run*<br/>
UPDATE: <b>The latest version at the time of writing (TX-2) was *JetPack-L4T-3-linux-x64.run</b><br/>
STEP 2: Connect HOST (*Ubuntu 14.04* or *Ubuntu 16.04 with JetPack 3*) machine to router (switch)<br/>
STEP 3: Connect Jetson (TX1/TX2) to router (switch)<br/>
STEP 4: Navigate to download folder of JetPack file and give executability rights to the installer file:<br/>

> $ chmod +x JetPack-L4T-(ver)-linux-x64.run

STEP 5: Run the installer file:<br/>

> $ ./JetPack-L4T-(ver)-linux-x64.run

STEP 6: Select Jetson platform when prompted (here: Jetson TX1/TX2 with Ubuntu Host)<br/>
STEP 7: Enter administrator password<br/>
STEP 8: Select Standard or Full in Component Manager and accept all Terms and Conditions<br/>
STEP 9: Once the installation completes on th
e Host machine, you will see a message "Completed Host installation, Installer will continue with Device/Post installation." <br/>
STEP 10: In the *networking layout* option, select the first option as mentioned in the above instructions (Device accesses Internet via router/switch.)<br/>
STEP 11: Put the Jetson TX1/TX2 in *Force USB Recovery Mode* by following the instructions on the screen<br/>
STEP 12: The device will proceed to get flashed. Wait until you see the message "Finished Flashing OS". Then hit the reset button on the device and wait till it enters the Ubuntu GUI.<br/>
STEP 13: Hit enter to continue on the host machine and set the IP address using ifconfig of prompted.<br/>
STEP 14: Remove all packages from the host (y/n) - decide accordingly<br/>

***

## Installing ROS Kinetic on TX-1 or TX-2

Installing ROS on the Tegra devices is pretty straightforward, following the instructions from the official ROS Installer Guidelines. <br/>

Inside this repository you will find an executable shell script named **ros-kinetic-install.sh**. This is a compilation of all the steps to install ROS Kinetic on your TX1/TX2. This script will install the barebones version of ROS-Kinetic. If you wish to install the full desktop version, comment out the script that installs the **ros-base** version and uncomment the desired version installer. <br/>

An additional note is in the initialization of **rosdep**. You may recieve a warning requiring you to fix your rosdep permission.<br/>

To do that, simply follow the instructions mentioned, i.e <br/>
> $ sudo rosdep fix-permissions

> $ rosdep update

At the end of the installer, you should be able to launch your **roscore** and view your rosnode list successfully!<br/>





***

## Verifying CUDA 8.0 installation
By installing JetPack, you should now be able to run CUDA and all the samples that come with it<br/>
STEP 1: To check if you have successfully intalled cuda - version should say CUDA 8.0<br/>
> $ nvcc -V

STEP 2: To run a sample, from the home directory<br/>
> $ cd ~/NVIDIA_CUDA-8.0_Samples/bin/aarch64/linux/release/

STEP 3: You should see a list of executable scripts for all the CUDA samples<br/>
> $ ./smokeParticles

You should see the example running! I noticed a frame rate of ~38fps for this example<br/>

![CUDAExample](https://github.com/ShreyasSkandan/nvidia-tx1/blob/master/imgs/smokeparticles.png)

***

## Verifying VisionWorks installation
In a similar manner you can test the Vision Works install<br/>
> $ cd ~/VisionWorks-SFM-0.88-Samples/bin/aarch64/linux/release/

> $./nvx_sample_sfm

You should see a running example of Structure From Motion in what appears to be a parking lot<br/>

![VisionWorksExample](https://github.com/ShreyasSkandan/nvidia-tx1/blob/master/imgs/sfm_screenshot.png)

On the NVIDIA TX-2, the process is slightly different. <br/>

The samples are saved in /usr/share/. You must move them to a desired location before you can build them.

> $ ./usr/share/visionworks/install_samples.sh ~

This will move the samples to your $HOME directory. Navigate to this folder and issue a <i>make</i> command to build all <b>VisionWorks-1.6</b> samples as shown above.

<b>NOTE:</b> At the time of writing, I was unsuccessful in installing VisionWorks 1.6 on my most machine. I was only able to install it on the TX-2. Code written in OpenVX using the NVXIO library will not move over perfectly from a TX-1 to the TX-2 because the NVXIO library has now been split into NVX and OVX, so editing of function calls and such will be required. </br>

***

## Verifying OpenCV installation
You can verify that openCV has been successfully installed by running a quick example. Refer to opencv_stuff/test-working/ for source code<br/>
STEP 1: Make sure you have a text editor (I use gedit)<br/>
STEP 2: Install cmake<br/>
> $ sudo apt-get install cmake

STEP 3: After creating helloworld.cpp and CMakeLists.txt create a build directory<br/>
> $ mkdir build

STEP 4: Enter build directory and run cmake<br/>
> $ cd build/
> $ cmake ..

STEP 5: Run the make command from the build directory<br/>
> $ make

STEP 5(o): If you encounter a missing library binding error such as this<br>
> /usr/bin/ld: cannot find -lopencv_dep_cudart

You might need to manually specify the location of the library before executing the make command<br/>
STEP 5(o): You can do this by navigating to the links.txt file <br/>
> $ cd ~/nvidia-tx1/opencv_stuff/test-working/build/CMakeFiles/cv_hello.dir/
> $ gedit links.txt

STEP 5(o): Replace -lopencv_dep_cudart with the location of the libcudart.so file (/usr/local/cuda-8.0/lib64/libcudart.so)<br/>

STEP 5(o): Run the make command from the build directory

STEP 6: You will generate an executable named cv_hello. You can now run the example and should see a similar output.<br/>
> $ ./cv_hello

<b>NOTE:</b> At the time of writing, JetPack 3 and OpenCV <b>(OpenCV4Tegra)</b> for the TX2 were compiled with the wrong GPU architecutre. Instead of <b>compute_62</b> and <b>sm_62</b> it has been compiled with <b>compute_53</b> and <b>sm_53</b> resulting in the failure to use any of opencv's gpu functions with OpenCV4Tegra. You can build OpenCV from source which is a work around for this problem until the next update.

![OpenCVExample](https://github.com/ShreyasSkandan/nvidia-tx1/blob/master/imgs/opencvexample.png)

***

## Installing Torch7 on NVIDIA TX1/TX2

To install Torch7 on the Jetson TX1/TX2, I recommend using [dusty-nv](https://github.com/dusty-nv)'s installation script.<br/>

Click [here](https://github.com/dusty-nv/jetson-reinforcement) to go to the Torch7 installation repository. Follow the instructions and you should have Torch7 successfully running on the TX1 in under 45 minutes. You can skip the gazebo install and that should make the process quicker.

The actual installation script can be found [here](https://github.com/dusty-nv/jetson-reinforcement/blob/master/CMakePreBuild.sh).

The above script did not automatically update my bash profile, so don't forget to do that if it hasn't done it for you automatically.

Adding the following to your $PATH variable should work:

> /home/ubuntu/jetson-reinforcement/build/torch/bin
***

## Using additional storage with the NVIDIA TX1

[![Alt text for your video](https://img.youtube.com/vi/6nzWt42mzqk/0.jpg)](http://www.youtube.com/watch?v=6nzWt42mzqk)
***

## Automatically mounting your storage device on the NVIDIA TX1

[![Alt text for your video](https://img.youtube.com/vi/F75NGzf7KvM/0.jpg)](http://www.youtube.com/watch?v=F75NGzf7KvM)
***

## Creating swapfile for extra performance

[![Alt text for your video](https://img.youtube.com/vi/pmJsLYlCy0w/0.jpg)](http://www.youtube.com/watch?v=pmJsLYlCy0w)
***

