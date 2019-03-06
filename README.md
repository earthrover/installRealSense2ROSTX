# installRealSense2ROSTX
Install the Intel RealSense Camera package for ROS on the NVIDIA Jetson TX Development Kit
<br>MIT License
<br>Copyright (c) 2018-19 Jetsonhacks

The installLibRealSenseROS script will install librealsense and realsense_camera as ROS packages. These scripts have been tested with a RealSense D435 camera.

This is the third step of a three step process.

The first step requires a kernel modification. librealsense 2 requires a modified kernel which modularizes uvcvideo and adds the RealSense video modes to the uvcvideo driver.

The easiest way to accomplish this is to use the 'buildLibrealsense2TX' repository on the Github JetsonHacks account (https://github.com/jetsonhacks/buildLibrealsense2TX). There are scripts which download the kernel source, apply the necessary patches, make the kernel, and then copy the kernel images to the boot directory. There are also scripts to build the librealsense library itself, which is useful for testing purposes.

The second step is to install ROS on the Jetson TX. There are convenience scripts to help do this on the Github JetsonHacks account in the installROSTX2 repository (https://github.com/jetsonhacks/installROSTX2) or installROSTX1 repository (https://github.com/jetsonhacks/installROSTX1). Note that the repository installs ros-base, if other configurations such as ros-desktop are desired, the scripts can do that through the command line parameters.

This step, the third step, is to install librealsense and realsense as ROS packages. The script installRealSenseROS.sh in this directory will install librealsense and realsense and dependencies in a Catkin Workspace.

This installs RealSense ROS version **2.0.3**

To install, the following lines assume you to have a workspace already set up in the **home** directory with the name `earth_rover_ws`.
	
	$ cd ~/earth_rover_ws
	$ git clone https://github.com/earthrover/installRealSense2ROSTX.git
	$ cd installRealSense2ROSTX
	$ ./installRealSenseROS.sh earth_rover_ws

A modified `.launch` file is attached to this repository. Copy the launch file into the ROS package. 

	$ cd ~/earth_rover_ws/installRealSense2ROSTX
	$ cp rs_camera_mod.launch ~/earth_rover_ws/src/realsense/realsense2_camera/launch	

To start the camera node in ROS:

	$ cd ~/earth_rover_ws/
	$ source devel/setup.bash
	$ roslaunch realsense2_camera rs_camera_mod.launch

More info about parameters, configuration and published topics can be found [here](https://github.com/intel-ros/realsense#usage-instructions)

The script 'setupTX.sh' simply turns off the USB autosuspend setting on the Jetson TX so that the camera is always available. 

<h3>Releases:</h3>

<b>February, 2019</b>
* v1.1
* Add support for catkin build workspaces (Thanks to Johann Lange)

<b>June, 2018</b>
* v1.0
* Initial Release
