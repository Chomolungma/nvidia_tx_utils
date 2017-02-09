# NVIDIA - TX1 
Repository of all NVIDIA TX-1 related code and usage instructions. 

## Initial Set-up
When you boot up the Jetson TX1 for the first time a terminal window will appear. To use the Ubuntu via the GUI, install the Nvidia Linux drive
Go to home directory (use username: **ubuntu** and password: **ubuntu**)<br/>
>$ cd NVIDIA-INSTALLER <br/>

>$ sudo ./installer.sh <br/>

After the installation completes:<br/>
>$ sudo reboot <br/>

You should now be able to log into the Ubuntu GUI

## Installing JetPack 
https://developer.nvidia.com/embedded/jetpack<br/>
* Download JetPack on the Host Machine by joining Embedded System Developer programme on NVIDIA page<br/>
* Latest at the time of writing : JetPack-L4T-2.3.1-linux-x64.run<br/>
* Connect HOST (Ubuntu 14.04) machine to router (switch)<br/>
* Connect Jetson (TX1) to router (switch)<br/>
* Navigate to download folder of JetPack file<br/>
* Give executability rights to the installer file:<br/>
> $ chmod +x JetPack-L4T-2.3.1-linux-x64.run

Run the installer file:<br/>
> $ ./JetPack-L4T-2.3.1-linux-x64.run

Select Jetson platform (here: Jetson TX1 with Ubuntu Host)<br/>
Enter administrator password<br/>
Select Standard | Full in Component Manager<br/>
Accept all Terms and Conditions<br/>
Once the installation completes on the Host machine, you will see a message "Completed Host installation, Installer will continue with Device/Post installation." <br/>
In the networking layout option, select the first option as mentioned in the above instructions ( Device accesses Internet via router/switch. )<br/>
Put the Jetson TX1 in Force USB Recovery Mode by following the instructions on the screen<br/>
The device will proceed to get flashed. Wait until you see the message "Finished Flashing OS". Then hit the reset button on the device and wait till it enters the Ubuntu GUI.<br/>
Hit enter to continue<br/>
Set the IP address using ifconfig<br/>
Remove all packages from the host (y/n) - decide accordingly<br/>

## Verifying CUDA 8.0 installation
By installing JetPack, you should now be able to run CUDA and all the samples that come with it<br/>
To check if you have successfully intalled cuda<br/>
> $ nvcc -V

To run a sample, from the home directory<br/>
> $ cd ~/NVIDIA_CUDA-8.0_Samples/bin/aarch64/linux/release/

You should see a list of executable scripts for all the CUDA samples<br/>
> $ ./smokeParticles

You should see the example running! I noticed a frame rate of ~38fps for this example<br/>


## Verifying VisionWorks installation
In a similar manner you can test the Vision Works install<br/>
> $ cd ~/VisionWorks/bin/aarch64/linux/release/

> $./mvx-sfm-test

You should see a running example of Structure From Motion in what appears to be a parking lot<br/>



