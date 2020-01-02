cmake_minimum_required(VERSION 3.12...3.16)

project(UpstreamLib)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_INCLUDE_CURRENT_DIR_IN_INTERFACE ON)

set(Upstream_VERSION 3.4.1)
set(include_dest "include/fruits-1.0")

include(GenerateExportHeader)

add_library(FruitsLib STATIC fruits.cpp)
generate_export_header(FruitsLib)
target_include_directories(FruitsLib
  PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
    "$<INSTALL_INTERFACE:${include_dest}>"
)
set_property(TARGET FruitsLib PROPERTY VERSION ${Upstream_VERSION})
#set_property(TARGET FruitsLib PROPERTY SOVERSION 3)
set_property(TARGET FruitsLib PROPERTY
  INTERFACE_FruitsLib_MAJOR_VERSION 3
)
set_property(TARGET FruitsLib APPEND PROPERTY
  COMPATIBLE_INTERFACE_STRING FruitsLib_MAJOR_VERSION
)

install(TARGETS FruitsLib EXPORT FruitsTargets
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
  INCLUDES DESTINATION include
)
install(
  FILES
    include/fruits/fruits.h
  DESTINATION
    include
  COMPONENT
    Devel
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/Fruits/FruitsConfigVersion.cmake"
  VERSION ${Upstream_VERSION}
  COMPATIBILITY AnyNewerVersion
)

export(EXPORT FruitsTargets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/Fruits/FruitsTargets.cmake"
  NAMESPACE Upstream::
)
configure_file(cmake/FruitsConfig.cmake
  "${CMAKE_CURRENT_BINARY_DIR}/Fruits/FruitsConfig.cmake"
  COPYONLY
)

set(ConfigPackageLocation lib/cmake/Fruits)
install(EXPORT FruitsTargets
  FILE
    FruitsTargets.cmake
  NAMESPACE
    Upstream::
  DESTINATION
    ${ConfigPackageLocation}
)
install(
  FILES
    cmake/FruitsConfig.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/Fruits/FruitsConfigVersion.cmake"
  DESTINATION
    ${ConfigPackageLocation}
  COMPONENT
    Devel
)
