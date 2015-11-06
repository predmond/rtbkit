cmake_minimum_required(VERSION 2.6)
project(RTBKit)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")

include_directories("/home/rtbkit/local/include")
include_directories("${PROJECT_SOURCE_DIR}/jml")
include_directories("${PROJECT_SOURCE_DIR}/soa")
include_directories("${PROJECT_SOURCE_DIR}")

link_directories("/home/rtbkit/local/lib")

add_library(tinyxml2 SHARED tinyxml2/tinyxml2.cpp)

add_subdirectory(googleurl)
add_subdirectory(jml)
add_subdirectory(rtbkit)
add_subdirectory(soa)
