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
```

* Possible packages installed
```
ros-humble-action-msgs* ros-humble-ament-cmake* ros-humble-ament-cmake-core*
  ros-humble-ament-cmake-export-definitions* ros-humble-ament-cmake-export-dependencies*
  ros-humble-ament-cmake-export-include-directories* ros-humble-ament-cmake-export-interfaces*
  ros-humble-ament-cmake-export-libraries* ros-humble-ament-cmake-export-link-flags*
  ros-humble-ament-cmake-export-targets* ros-humble-ament-cmake-gen-version-h*
  ros-humble-ament-cmake-gmock* ros-humble-ament-cmake-gtest*
  ros-humble-ament-cmake-include-directories* ros-humble-ament-cmake-libraries*
  ros-humble-ament-cmake-pytest* ros-humble-ament-cmake-python* ros-humble-ament-cmake-ros*
  ros-humble-ament-cmake-target-dependencies* ros-humble-ament-cmake-test*
  ros-humble-ament-cmake-version* ros-humble-ament-index-cpp* ros-humble-ament-index-python*
  ros-humble-ament-package* ros-humble-builtin-interfaces* ros-humble-camera-calibration-parsers*
  ros-humble-camera-info-manager* ros-humble-class-loader* ros-humble-console-bridge-vendor*
  ros-humble-cv-bridge* ros-humble-domain-coordinator* ros-humble-fastcdr* ros-humble-fastrtps*
  ros-humble-fastrtps-cmake-module* ros-humble-foonathan-memory-vendor* ros-humble-geometry-msgs*
  ros-humble-gmock-vendor* ros-humble-gtest-vendor* ros-humble-image-transport*
  ros-humble-libstatistics-collector* ros-humble-libyaml-vendor* ros-humble-lifecycle-msgs*
  ros-humble-message-filters* ros-humble-pluginlib* ros-humble-python-cmake-module*
  ros-humble-rcl* ros-humble-rcl-action* ros-humble-rcl-interfaces* ros-humble-rcl-lifecycle*
  ros-humble-rcl-logging-interface* ros-humble-rcl-logging-spdlog*
  ros-humble-rcl-yaml-param-parser* ros-humble-rclcpp* ros-humble-rclpy* ros-humble-rcpputils*
  ros-humble-rcutils* ros-humble-rmw* ros-humble-rmw-dds-common* ros-humble-rmw-fastrtps-cpp*
  ros-humble-rmw-fastrtps-shared-cpp* ros-humble-rmw-implementation*
  ros-humble-rmw-implementation-cmake* ros-humble-ros-workspace* ros-humble-rosgraph-msgs*
  ros-humble-rosidl-adapter* ros-humble-rosidl-cli* ros-humble-rosidl-cmake*
  ros-humble-rosidl-default-runtime* ros-humble-rosidl-generator-c*
  ros-humble-rosidl-generator-cpp* ros-humble-rosidl-generator-py* ros-humble-rosidl-parser*
  ros-humble-rosidl-runtime-c* ros-humble-rosidl-runtime-cpp* ros-humble-rosidl-typesupport-c*
  ros-humble-rosidl-typesupport-cpp* ros-humble-rosidl-typesupport-fastrtps-c*
  ros-humble-rosidl-typesupport-fastrtps-cpp* ros-humble-rosidl-typesupport-interface*
  ros-humble-rosidl-typesupport-introspection-c* ros-humble-rosidl-typesupport-introspection-cpp*
  ros-humble-rpyutils* ros-humble-sensor-msgs* ros-humble-spdlog-vendor*
  ros-humble-statistics-msgs* ros-humble-std-msgs* ros-humble-tinyxml2-vendor*
  ros-humble-tracetools* ros-humble-unique-identifier-msgs* ros-humble-yaml-cpp-vendor*
```