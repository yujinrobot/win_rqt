cmake_minimum_required(VERSION 2.8)
project(win_rqt)
find_package(catkin REQUIRED COMPONENTS catkin)
catkin_package()

################################################################
# Macros
################################################################

macro(add_python_exe_helper name)
  # make the target name unique so we don't clash (e.g. rosbag target)
  add_executable(${name}_exe src/ros_bin.cpp)
  # ensure the output name isn't mucked up by the unique target name.
  set_target_properties(${name}_exe PROPERTIES OUTPUT_NAME ${name})
  set_target_properties(${name}_exe PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CATKIN_DEVEL_PREFIX}/${CATKIN_GLOBAL_BIN_DESTINATION})
  install(TARGETS ${name}_exe RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION})
endmacro()

################################################################
# Python Helpers
################################################################

set(NAMES rqt rqt_bag rqt_console rqt_graph rqt_logger_level rqt_plot)

include_directories(${catkin_INCLUDE_DIRS})

foreach(name ${NAMES})
  add_python_exe_helper(${name})
endforeach()
