cmake_minimum_required(VERSION 2.8.3)
project(tinyxml)
find_package(catkin REQUIRED COMPONENTS)
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES tinyxml
)

include_directories(include ${catkin_INCLUDE_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

if(WIN32)
  add_definitions(-D_WINDOWS)
endif()

add_definitions( -DTIXML_USE_STL)

add_library(tinyxml
  src/tinystr.cpp
  src/tinyxml.cpp
  src/tinyxmlerror.cpp
  src/tinyxmlparser.cpp
  )

# FIXME the headers should be in a package-specific subfolder but can not be for backward compatibility
install(DIRECTORY include/
  DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h")

install(TARGETS tinyxml
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION})
