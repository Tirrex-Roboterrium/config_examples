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
project and put them outside of this repos (in the `demos` directory but not `demos/examples`).

In each demo directory, there is a hidden `.env` file that corresponds to a symbolic link to the
`.env` at the root of the workspace.
It contains some environment variables required by the docker compose configuration.
Because you have created a new directory, you have to update the path of `.env` to correctly point
to the `.env` at the root of the workspace.
For example, if you directly put your demo directory into `demos`, the path should be `../../.env`.
From your demo direcotry, execute
```
ln -sfr ../../.env .
```
