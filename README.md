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
