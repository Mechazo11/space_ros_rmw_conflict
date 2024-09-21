# RMW_CONFLICT

This repository contains a docker file that will generate a fatal error caused by ```rmw_cyclonedds_cpp``` and ```rmw_implementation```. I discovered this when integrating Open 3D Engine with Space ROS. This error is caused when ROS 2 Gem within O3DE looks for an implementation of DDS, which by default in space ros, is ```cyclonedds```.

**NOTE** please allot 30GB disk space and about 20-25 mins for the image to build.

## Instructions

* Pull the latest copy of ```osrf/space-ros``` image: ```docker pull osrf/space-ros```

* Build the image: ```docker build -t rmw_conflict -f Dockerfile_rmw_conflict .```

* Open a container: ```docker run -it rmw_conflict /bin/bash```

* Execute the following commands in the container's terminal

```bash
source /opt/ros/humble/setup.bash
source $SPACEROS_DIR/install/setup.bash
cmake -B build/linux -G "Ninja Multi-Config" -DLY_DISABLE_TEST_MODULES=ON -DCMAKE_EXPORT_COMPILE_COMMANDS=ON -DLY_STRIP_DEBUG_SYMBOLS=ON -DAZ_USE_PHYSX5:BOOL=ON
```

* The generated error will look like the following

```shell
-- Ros Distro is "humble"
-- Found rclcpp: 16.0.10 (/home/spaceros-user/spaceros/install/rclcpp/share/rclcpp/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found rmw_implementation_cmake: 6.1.2 (/home/spaceros-user/spaceros/install/rmw_implementation_cmake/share/rmw_implementation_cmake/cmake)
-- Found rmw_cyclonedds_cpp: 1.3.4 (/home/spaceros-user/spaceros/install/rmw_cyclonedds_cpp/share/rmw_cyclonedds_cpp/cmake)
-- Using RMW implementation 'rmw_cyclonedds_cpp'
-- Found builtin_interfaces: 1.2.1 (/home/spaceros-user/spaceros/install/builtin_interfaces/share/builtin_interfaces/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found std_msgs: 4.2.4 (/home/spaceros-user/spaceros/install/std_msgs/share/std_msgs/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found sensor_msgs: 4.2.4 (/home/spaceros-user/spaceros/install/sensor_msgs/share/sensor_msgs/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found nav_msgs: 4.2.4 (/home/spaceros-user/spaceros/install/nav_msgs/share/nav_msgs/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found tf2_ros: 0.25.7 (/home/spaceros-user/spaceros/install/tf2_ros/share/tf2_ros/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found rmw_implementation_cmake: 6.1.2 (/home/spaceros-user/spaceros/install/rmw_implementation_cmake/share/rmw_implementation_cmake/cmake)
-- Found rmw_cyclonedds_cpp: 1.3.4 (/home/spaceros-user/spaceros/install/rmw_cyclonedds_cpp/share/rmw_cyclonedds_cpp/cmake)
-- Using RMW implementation 'rmw_cyclonedds_cpp'
CMake Error at /home/spaceros-user/spaceros/install/rmw_implementation/share/rmw_implementation/cmake/rmw_implementation-extras.cmake:34 (add_library):
  add_library cannot create imported target
  "rmw_implementation::rmw_implementation" because another target with the
  same name already exists.
Call Stack (most recent call first):
  /home/spaceros-user/spaceros/install/rmw_implementation/share/rmw_implementation/cmake/rmw_implementationConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/rcl/share/rcl/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/rcl/share/rcl/cmake/rclConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/libstatistics_collector/share/libstatistics_collector/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/libstatistics_collector/share/libstatistics_collector/cmake/libstatistics_collectorConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/rclcpp/share/rclcpp/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/rclcpp/share/rclcpp/cmake/rclcppConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/rclcpp_components/share/rclcpp_components/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/rclcpp_components/share/rclcpp_components/cmake/rclcpp_componentsConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/tf2_ros/share/tf2_ros/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/tf2_ros/share/tf2_ros/cmake/tf2_rosConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/o3de-extras/Gems/ROS2/Code/ros2_target_depends.cmake:8 (find_package)
  /home/spaceros-user/spaceros/o3de-extras/Gems/ROS2/Code/ros2_target_depends.cmake:20 (target_depends_on_ros2_package)
  /home/spaceros-user/spaceros/o3de-extras/Gems/ROS2/Code/CMakeLists.txt:72 (target_depends_on_ros2_packages)

-- Found ackermann_msgs: 2.0.2 (/opt/ros/humble/share/ackermann_msgs/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found gazebo_msgs: 3.7.0 (/opt/ros/humble/share/gazebo_msgs/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found control_toolbox: 3.2.0 (/home/spaceros-user/spaceros/install/control_toolbox/share/control_toolbox/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Found rmw_implementation_cmake: 6.1.2 (/home/spaceros-user/spaceros/install/rmw_implementation_cmake/share/rmw_implementation_cmake/cmake)
-- Found rmw_cyclonedds_cpp: 1.3.4 (/home/spaceros-user/spaceros/install/rmw_cyclonedds_cpp/share/rmw_cyclonedds_cpp/cmake)
-- Using RMW implementation 'rmw_cyclonedds_cpp'
CMake Error at /home/spaceros-user/spaceros/install/rmw_implementation/share/rmw_implementation/cmake/rmw_implementation-extras.cmake:34 (add_library):
  add_library cannot create imported target
  "rmw_implementation::rmw_implementation" because another target with the
  same name already exists.
Call Stack (most recent call first):
  /home/spaceros-user/spaceros/install/rmw_implementation/share/rmw_implementation/cmake/rmw_implementationConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/rcl/share/rcl/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/rcl/share/rcl/cmake/rclConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/libstatistics_collector/share/libstatistics_collector/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/libstatistics_collector/share/libstatistics_collector/cmake/libstatistics_collectorConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/rclcpp/share/rclcpp/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/rclcpp/share/rclcpp/cmake/rclcppConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/install/control_toolbox/share/control_toolbox/cmake/ament_cmake_export_dependencies-extras.cmake:21 (find_package)
  /home/spaceros-user/spaceros/install/control_toolbox/share/control_toolbox/cmake/control_toolboxConfig.cmake:41 (include)
  /home/spaceros-user/spaceros/o3de-extras/Gems/ROS2/Code/ros2_target_depends.cmake:8 (find_package)
  /home/spaceros-user/spaceros/o3de-extras/Gems/ROS2/Code/CMakeLists.txt:73 (target_depends_on_ros2_package)

-- Found parameter_traits: 0.3.8 (/home/spaceros-user/spaceros/install/parameter_traits/share/parameter_traits/cmake)
-- Found rclcpp_lifecycle: 16.0.10 (/home/spaceros-user/spaceros/install/rclcpp_lifecycle/share/rclcpp_lifecycle/cmake)
-- Downloading package into /home/spaceros-user/.o3de/3rdParty/packages/sdformat-13.5.0-rev2-linux
'/usr/bin/cmake' '-E' 'tar' 'xf' '/home/spaceros-user/.o3de/3rdParty/downloaded_packages/sdformat-13.5.0-rev2-linux.tar.xz'
-- Installed And Validated package at /home/spaceros-user/.o3de/3rdParty/packages/sdformat-13.5.0-rev2-linux - OK
-- Using package /home/spaceros-user/.o3de/3rdParty/packages/sdformat-13.5.0-rev2-linux
-- Found geometry_msgs: 4.2.4 (/home/spaceros-user/spaceros/install/geometry_msgs/share/geometry_msgs/cmake)
-- Using all available rosidl_typesupport_c: rosidl_typesupport_introspection_c;rosidl_typesupport_fastrtps_c
-- Found rosidl_adapter: 3.1.5 (/home/spaceros-user/spaceros/install/rosidl_adapter/share/rosidl_adapter/cmake)
-- Using all available rosidl_typesupport_cpp: rosidl_typesupport_introspection_cpp;rosidl_typesupport_fastrtps_cpp
-- Downloading package into /home/spaceros-user/.o3de/3rdParty/packages/OpenMesh-8.1-rev3-linux
'/usr/bin/cmake' '-E' 'tar' 'xf' '/home/spaceros-user/.o3de/3rdParty/downloaded_packages/OpenMesh-8.1-rev3-linux.tar.xz'
-- Installed And Validated package at /home/spaceros-user/.o3de/3rdParty/packages/OpenMesh-8.1-rev3-linux - OK
-- Using package /home/spaceros-user/.o3de/3rdParty/packages/OpenMesh-8.1-rev3-linux
-- Configuring incomplete, errors occurred!
```