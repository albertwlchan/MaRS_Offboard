# SVARM Project
This branch is used to replace localization with a optitrack motion capture system with Visual Inertial Odometry using a intel realsense t265 camera.
Code based on https://github.com/thien94/vision_to_mavros
## Packages under src/

`mavros`-communication with pixhawk4

`realsense-ros`-read the realsense camera pose
 
`offboard`-generate the path and pass to px4

`mavlink`-the communication protocol of pixhawk4

`vision_to_mavros`- remaps the realsense camera pose topic `"/camera_link"` to `/mavros/vision_pose/pose`

## Installation and Setup

1. Install librealsense by following instructions on https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md

	a)If using manifold 2C (Intel CPU), follow instructions as normal.

	b)If using manifold 2G (Nvidia Jetson GPU), use `sudo apt-get install librealsense2-dev`
	instead of `sudo apt-get install librealsense2-dkms`. For more info, refer to https://github.com/IntelRealSense/librealsense/blob/master/doc/installation_jetson.md

2. Install ddynamic_reconfigure using `sudo apt-get update apt-get install ros-kinetic-ddynamic-reconfigure`

3. In QGCcontrol, follow steps here https://dev.px4.io/v1.9.0/en/ros/external_position_estimation.html#ekf2-tuningconfiguration

	a) Set EKF2_AID_MASK to vision position fusion and vision yaw fusion

	b) Set EKF2_HGT_MODE to Vision to use the vision a primary source for altitude estimation.

	c) Set EKF2_EV_POS_X, EKF2_EV_POS_Y, EKF2_EV_POS_Z with the position of the vision sensor with respect to the robot's body frame using ned convention.

	d) (Optional) Set EKF2_EV_DELAY if needed

## Normal Steps

1. `cd MaRS_Offboard`
2. `catkin build`
3. `source devel/setup.bash`
4. `roslaunch vision_to_mavros t265_all_nodes.launch` Launches rs_t265.launch, px4.launch, and t265_tf_to_mavros.launch

after these steps, position control of the drone using VIO will work.



