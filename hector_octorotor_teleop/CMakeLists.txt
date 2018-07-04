cmake_minimum_required(VERSION 2.8.3)
project(hector_octorotor_teleop)


find_package(catkin REQUIRED COMPONENTS
  actionlib
  roscpp
  sensor_msgs
  geometry_msgs
  hector_octorotor_interface
  tf2_geometry_msgs
  visualization_msgs)
include_directories(include ${catkin_INCLUDE_DIRS})

catkin_package(
    INCLUDE_DIRS
    LIBRARIES
    CATKIN_DEPENDS roscpp sensor_msgs geometry_msgs hector_uav_msgs
    DEPENDS
)

add_executable(octorotor_teleop src/octorotor_teleop.cpp)
target_link_libraries(octorotor_teleop ${catkin_LIBRARIES})
add_dependencies(octorotor_teleop ${catkin_EXPORTED_TARGETS})

install(TARGETS octorotor_teleop
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch
  DESTINATION  ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
