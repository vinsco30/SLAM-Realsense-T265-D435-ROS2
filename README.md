# Docker for RealSense T265 for ROS2
Compiling the docker file, it is possible to use the Realsense T265 with ROS2. 
The container will run ROS2 Foxy but the implementation of the CycloneDDS allows to share the topics
with ROS2 Humble too. 


## Details

- **Auto-deletion:** After its execution, the Docker container is automatically deleted. This helps in maintaining a clean environment by freeing up resources on the host machine.

- **`ros2_ws-src` folder:** This folder should contain the source code for the ROS2 workspace. The Docker container comes pre-loaded with a custom version of `realsense-ros` package where the QoS of the output topics are already set as `BEST_EFFORT`.

- **`ROS_DOMAIN_ID`:** it is set by default as 69, you can change it in the dockerfile before building the image.

### Prerequisites

What things you need to install the software and how to install them:

- Docker 

### Installing

A step by step series of examples that tell you how to get a development environment running:

1. Clone the repository to your local machine.
2. Build the docker imagege with `cd docker && docker build -t ov-rs-ros2-foxy -f ov_foxy_rs_dockerfile.txt .`
3. Run the container with `./run_cnt.sh`.

## Running the Realsense node

Once the container is running, source the workspace,

        $ . ros2_ws/install/local_setup.bash $

Now you can plug the T265 cam and run the node,

        $ ros2 launch realsense2_camera rs_t265_launch.py $

### TODO: lighten up the image