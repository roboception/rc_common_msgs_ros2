cmake_minimum_required(VERSION 3.5)

project(rc_common_msgs)
include(cmake/project_version.cmake)

# - Configuration for code optimization -
if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE RELEASE CACHE STRING "Build type: DEBUG or RELEASE" FORCE)
endif ()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)

set(msg_files
  "msg/CameraParam.msg"
  "msg/KeyValue.msg"
  "msg/ReturnCode.msg"
  "msg/ReturnCodeConstants.msg"
)

set(srv_files
  "srv/Trigger.srv"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  DEPENDENCIES std_msgs
  ADD_LINTER_TESTS
)

ament_export_dependencies(rosidl_default_runtime)

ament_package()

######################################
## Define information for packaging ##
######################################
set(CPACK_DEBIAN_PACKAGE_SHLIBDEPS OFF)
include(cmake/package_debian.cmake)
