cmake_minimum_required(VERSION 2.8.3)
project(hector_octorotor_interface)

find_package(catkin REQUIRED COMPONENTS roscpp geometry_msgs sensor_msgs nav_msgs hector_uav_msgs std_srvs hardware_interface controller_interface tf2 tf2_geometry_msgs urdf)
include_directories(include ${catkin_INCLUDE_DIRS})

find_package(Boost REQUIRED COMPONENTS system)

catkin_package(
    INCLUDE_DIRS include
    LIBRARIES hector_octorotor_interface
    CATKIN_DEPENDS roscpp geometry_msgs sensor_msgs nav_msgs hector_uav_msgs std_srvs hardware_interface controller_interface
    DEPENDS
)

add_library(hector_octorotor_interface src/octorotor_interface.cpp src/helpers.cpp)
target_link_libraries(hector_octorotor_interface ${catkin_LIBRARIES})
add_dependencies(hector_octorotor_interface hector_uav_msgs_generate_messages_cpp)

install(TARGETS hector_octorotor_interface
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
)
