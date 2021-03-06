################################################################################
# CMake
################################################################################
cmake_minimum_required(VERSION 2.8.3)
project(dynamixel_sdk)

################################################################################
# Packages
################################################################################
find_package(catkin REQUIRED COMPONENTS
  roscpp
)

################################################################################
# Declare ROS messages, services and actions
################################################################################

################################################################################
# Declare ROS dynamic reconfigure parameters
################################################################################

################################################################################
# Catkin specific configuration
################################################################################
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES dynamixel_sdk
)

################################################################################
# Build
################################################################################
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_library(dynamixel_sdk
  src/${PROJECT_NAME}/packet_handler.cpp
  src/${PROJECT_NAME}/protocol1_packet_handler.cpp
  src/${PROJECT_NAME}/protocol2_packet_handler.cpp
  src/${PROJECT_NAME}/group_sync_read.cpp
  src/${PROJECT_NAME}/group_sync_write.cpp
  src/${PROJECT_NAME}/group_bulk_read.cpp
  src/${PROJECT_NAME}/group_bulk_write.cpp
  src/${PROJECT_NAME}/port_handler.cpp
  src/${PROJECT_NAME}_linux/port_handler_linux.cpp
)
add_dependencies(dynamixel_sdk ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(dynamixel_sdk ${catkin_LIBRARIES})

################################################################################
# Install
################################################################################
install(TARGETS dynamixel_sdk
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)

################################################################################
# Test
################################################################################
