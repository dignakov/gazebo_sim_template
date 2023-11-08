## Launch

A few launch files:

* `load_robot.launch` loads the description to the param server.

* `test_robot.launch` loads the robot and starts rviz.

* `gazebo.launch` loads an empty gazebo world, loads the robot onto the param server, and places the robot into the simulation.

* `controllers.launch` starts the controllers. This should be used after a simulation is running.

* `launch_gazebo_control.launch` launches gazebo and the controllers together for convenience.


## Modifying the model

`robot.urdf` contains all the basic structure for a robot like the amiga.

Adjust dimensions and inertia parameters, as well as the joint positions to match the real system.

The Clearpath package is a good source for how to use the proper visual meshes (https://github.com/husky/husky/tree/noetic-devel/husky_description), for example:


```
  <link name="base_link">
    <visual>
      <origin xyz="0 0 0" rpy="0 0 0" />
      <geometry>
        <mesh filename="package://husky_description/meshes/base_link.dae" />
      </geometry>
    </visual>
    <collision>
      <origin xyz="${( husky_front_bumper_extend - husky_rear_bumper_extend ) / 2.0} 0 ${base_z_size/4}" rpy="0 0 0" />
      <geometry>
        <box size="${ base_x_size + husky_front_bumper_extend + husky_rear_bumper_extend } ${base_y_size} ${base_z_size/2}"/>
      </geometry>
    </collision>
    <collision>
      <origin xyz="0 0 ${base_z_size*3/4-0.01}" rpy="0 0 0" />
      <geometry>
        <box size="${base_x_size*4/5} ${base_y_size} ${base_z_size/2-0.02}"/>
      </geometry>
    </collision>
  </link>

```

### URDF

Everything was included in the urdf. It's more common to have several xacro files to split up what information goes where. This is shown in both the ros urdf example, and the Gazebo one.

* https://wiki.ros.org/urdf/Tutorials

* https://classic.gazebosim.org/tutorials?tut=ros_urdf&cat=connect_ros


## Config

Minimal config examples, just enough to see the robot in rviz, and to use ros-control.

Effort controllers are the default in gazebo, individual joints can be controlled, or one controller can be used for groups of joints. Not all controllers are available in a group version (https://wiki.ros.org/ros_control)



## References:
https://github.com/husky/husky/tree/noetic-devel/husky_description
https://github.com/husky/husky/blob/noetic-devel/husky_description/urdf/husky.urdf.xacro
https://wiki.ros.org/Robots/Husky
https://clearpathrobotics.com/blog/2013/11/husky-simulation-in-gazebo/
https://classic.gazebosim.org/tutorials?tut=ros_urdf&cat=connect_ros
https://github.com/ros-simulation/gazebo_ros_demos/tree/kinetic-devel
https://wiki.ros.org/ros_control
