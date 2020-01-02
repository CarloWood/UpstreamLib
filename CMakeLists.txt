cmake_minimum_required(VERSION 3.16)

project(fruits_Lib)

add_library(fruits_Lib STATIC)

target_sources(fruits_Lib
  PRIVATE
    "fruits.cpp"
)

target_include_directories(fruits_Lib
  INTERFACE
    "${CMAKE_CURRENT_SOURCE_DIR}/include"
)

add_library(fruits::fruits ALIAS fruits_Lib)

