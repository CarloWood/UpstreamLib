cmake_minimum_required(VERSION 3.16)

project(fruits_Lib)

add_library(fruits_Lib STATIC)

target_sources(fruits_Lib
  PRIVATE
    "fruits.cpp"
)

set(include_dest "include/fruits-1.0")
set(main_lib_dest "lib/fruits-1.0")
set(lib_dest "${main_lib_dest}/${CMAKE_BUILD_TYPE}")

target_include_directories(fruits_Lib
  PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
    "$<INSTALL_INTERFACE:${include_dest}>"
)

add_library(fruits::fruits ALIAS fruits_Lib)

install(TARGETS fruits_Lib EXPORT fruits DESTINATION "${main_lib_dest}")
install(FILES "include/fruits/fruits.h" DESTINATION "${include_dest}")
install(EXPORT fruits::fruits DESTINATION "${lib_dest}")

