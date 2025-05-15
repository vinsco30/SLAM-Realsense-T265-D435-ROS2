# Docker for RealSense T265 for ROS2 + Localization 
Compiling the docker file, it is possible to use the Realsense T265 with ROS2. 
The container will run ROS2 Foxy but the implementation of the CycloneDDS allows to share the topics
with ROS2 Humble too. 


## Details

- **Auto-deletion:** After its execution, the Docker container is automatically deleted. This helps in maintaining a clean environment by freeing up resources on the host machine.

- **`ros2_ws-src` folder:** This folder should contain the source code for the ROS2 workspace. The Docker container comes pre-loaded with a custom version of `realsense-ros` package where the QoS of the output topics are already set as `BEST_EFFORT`.

- **`ROS_DOMAIN_ID`:** it is set by default as 68, you can change it in the dockerfile before building the image.

### Prerequisites

What things you need to install the software and how to install them:

- Docker 

### Installing

A step by step series of examples that tell you how to get a development environment running:

1. Clone the repository to your local machine.
2. Build the docker imagege with `cd docker && docker build -t ov-rs-ros2-foxy -f ov_foxy_rs_dockerfile.txt .`
3. Run the container with `./run_cnt.sh`.

## Running the Realsense node

You can plug the T265 cam and run the node,

        ros2 launch realsense2_camera rs_t265_launch.py 

If you want to run T265 + D435, run,

        ros2 launch realsense2_camera rs_d400_and_t265_launch.py

P.S. Modify the `tf_static_publisher` in the launch file for your cameras configurations

Launch the SLAM node,

        ros2 launch realsense2_camera rtabmap.launch.py 

## Running on the drone
If you want to run the camera configuration on your drone, there is the ad-hoc launch file

        ros2 launch realsense2_camera rs_d400_and_t265_drone_launch.py 

in this way you can launch your tf configuration for your robot, using for example the repository [Odometry launch package](https://github.com/vinsco30/odometry-launch-pkg)



### TODO: lighten up the image