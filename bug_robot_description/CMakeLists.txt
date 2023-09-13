cmake_minimum_required(VERSION 3.8)
project(bug_robot_description)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(gazebo REQUIRED)
find_package(gazebo_ros_pkgs REQUIRED)

add_executable(talker src/publisher_node.cpp)
ament_target_dependencies(talker rclcpp std_msgs sensor_msgs geometry_msgs)

link_directories(
  ${GAZEBO_LIBRARY_DIRS}
)

include_directories(
  include
  ${GAZEBO_INCLUDE_DIRS}
)

install(
  DIRECTORY launch meshes urdf 
  DESTINATION share/${PROJECT_NAME}
)

ament_export_dependencies(gazebo_ros_pkgs)

install(TARGETS
  talker
  DESTINATION lib/${PROJECT_NAME})

ament_package()
