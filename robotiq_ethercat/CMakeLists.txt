cmake_minimum_required(VERSION 2.8.3)
project(robotiq_ethercat)

add_compile_options(/std:c++latest)
add_definitions("/D_CRT_SECURE_NO_WARNINGS")
add_definitions("/D__STDC_LIMIT_MACROS")
add_definitions("/D_SILENCE_ALL_CXX17_DEPRECATION_WARNINGS")

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rosconsole
)

find_package(soem REQUIRED)

catkin_package(
   INCLUDE_DIRS include
   LIBRARIES robotiq_ethercat
   CATKIN_DEPENDS roscpp rosconsole
)

include_directories(include
  ${catkin_INCLUDE_DIRS}
  ${soem_INCLUDE_DIRS}
)

add_library(robotiq_ethercat
 include/robotiq_ethercat/ethercat_manager.h
 src/ethercat_manager.cpp
)

target_link_libraries(robotiq_ethercat ${catkin_LIBRARIES} ${soem_LIBRARIES})

install(TARGETS robotiq_ethercat
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
 )

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
)
