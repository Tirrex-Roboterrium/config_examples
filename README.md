This repository contains several demo configuration directories to show how to use all the robot in
simulation or using the real ones.
If you want to make some changes, **do not modify these files**.
Instead, copy one of them in the `demos` directory of your workspace to create your own config.

## Composition of a demo directory

A demo directory contains the following files:
* `compose.yaml`: this is the entrypoint of the demo.
    This file contains the `ros2 launch` commands to start the programs.
    For example, you can start all the services described in this file using `docker compose up`
* `config`: this directory contains all the yaml file to configure the ros nodes and also other
    configuration files (like rviz, zenoh, cyclone_dds, ...)
* `config/robot`: this subdirectory contains the configuration of a specific robot.
    When there are several robots in a same demo, this directory have is named `config/<robot_name>`
* `config/paths`: this subdirectory contains the paths to follow with the robot using GNSS
    Its format is described in
    [tiara_format.md](https://github.com/Romea/romea-ros-path-tools/blob/main/doc/tiara_format.md)
* `.env`: a symbolic link to the `.env` file at the root of the workspace.
    This file is mandatory to load environment variables defined in `compose.yaml`.


## How to create your own demo

The easiest way to create your own demo directory is to copy one of the directory defined in this
project and put them outside of this repos (in the `demos` directory).
After copying the desired demo, edit the `compose.yaml` file to adapt the value of `file:`.
This value corresponds to the relative path of `docker/full.yaml` (when `TIRREX_IMAGE_TAG == full`)
from your demo directory.
There is also other variables that may contain information specific to the demo like `DEMO_NAME` or
`ROS_LOG_DIR`.
For example, if I copy `demos/examples/simu_adap2e` to create `demos/my_simu`, the begining of
`compose.yaml` should look like this:
```yaml
x-yaml-anchors:
  base: &base
    extends:
      file: ../../docker/${TIRREX_IMAGE_TAG}.yaml  # the difference is '../../' instead of '../../../'
      service: x11_base
    volumes:
      - ./config:/config
    environment:
      - CONFIG_DIR=/config
      - ROBOT_CONFIG_DIR=/config/robot
      - DEMO_MODE=simulation_gazebo_classic
      - DEMO_NAME=my_simu                    # this name should be the name of the directory
      - ROBOT_NAMESPACE=robot
      - ROS_LOG_DIR=data/my_simu/log         # the name of the directory also appears here
```

After that, the demo will run correctly.
You can then edit the configuration to make your own version of the copied demo.
