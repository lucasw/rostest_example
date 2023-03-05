cmake_minimum_required(VERSION 3.0.2)
project(rostest_example)

find_package(catkin REQUIRED COMPONENTS
  message_generation
  message_runtime
  roscpp
  rospy
  sensor_msgs
  std_msgs
)

add_message_files(
   FILES
   ScanPoints.msg
   Line.msg
)

generate_messages(
  DEPENDENCIES
  sensor_msgs
  std_msgs
)

catkin_package(
)

catkin_install_python(PROGRAMS
  scripts/wall_detector.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

if(CATKIN_ENABLE_TESTING)
  find_package(rostest REQUIRED)

  add_rostest(test/wall_detector.test
    DEPENDENCIES ${${PROJECT_NAME}_EXPORTED_TARGETS})

  install(DIRECTORY test/ DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/test)
endif()

