cmake_minimum_required(VERSION 2.8.3)
project(aubo_kinematics)

add_compile_options(-std=c++11)
find_package(catkin REQUIRED COMPONENTS roscpp geometry_msgs moveit_core moveit_kinematics moveit_ros_planning_interface moveit_ros_planning pluginlib tf_conversions)
if("$ENV{ROS_DISTRO}" STREQUAL "kinetic")
    find_package(catkin REQUIRED COMPONENTS roscpp geometry_msgs moveit_core moveit_kinematics moveit_ros_planning_interface
      moveit_ros_planning pluginlib tf_conversions)
    Message(STATUS "<<<<<<<<<<<<<<<<<<<<<<<<<Note: Find Package for kinetic in kinematics build")
endif()


find_package(Boost REQUIRED COMPONENTS system)


catkin_package(
  INCLUDE_DIRS include
  LIBRARIES aubo_i10_kinematic aubo_i10_moveit_kinematic_plugin
  CATKIN_DEPENDS roscpp geometry_msgs moveit_core moveit_ros_planning
                 pluginlib tf_conversions
  DEPENDS boost
)


###########
## Build ##
###########

include_directories(SYSTEM ${Boost_INCLUDE_DIR})
include_directories(include ${catkin_INCLUDE_DIRS})


add_library(aubo_i10_kinematic src/kinematics.cpp)
set_target_properties(aubo_i10_kinematic PROPERTIES COMPILE_DEFINITIONS "AUBO_I10_PARAMS")


add_library(aubo_i10_moveit_kinematic_plugin src/aubo_moveit_plugin.cpp)
target_link_libraries(aubo_i10_moveit_kinematic_plugin
  ${catkin_LIBRARIES}
  ${Boost_LIBRARIES}
  aubo_i10_kinematic)


#############
## Install ##
#############

install(TARGETS aubo_i10_kinematic aubo_i10_moveit_kinematic_plugin
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# install header files
install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)

# install moveit plugin description file
install(FILES aubo_moveit_plugins.xml
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

