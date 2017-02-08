# NVIDIA - TX1 
Repository of all NVIDIA TX-1 related code and usage instructions. 

1. When you boot up the Jetson TX1 for the first time a terminal window will appear. To use the Ubuntu via the GUI, install the Nvidia Linux driver.
	* Go to home directory (use username: ubuntu and password: ubuntu)
	* '''' $ cd NVIDIA-INSTALLER ''''
	* > $ sudo ./installer.sh
	* After the installation completes:
	* > $ sudo reboot
	* You should now be able to log into the Ubuntu GUI

2. JetPack - https://developer.nvidia.com/embedded/jetpack
	* Download JetPack on the Host Machine by joining Embedded System Developer programme on NVIDIA page
	* Latest at the time of writing : JetPack-L4T-2.3.1-linux-x64.run
	* Connect HOST (Ubuntu 14.04) machine to router (switch)
	* Connect Jetson (TX1) to router (switch)
	* Navigate to download folder of JetPack file
	* Give executability rights to the installer file:
	* > $ chmod +x JetPack-L4T-2.3.1-linux-x64.run
	* Run the installer file:
	* > $ ./JetPack-L4T-2.3.1-linux-x64.run
3. 
