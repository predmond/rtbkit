cmake_minimum_required(VERSION 2.6)
project(RTBKit)

enable_testing()

function(add_rtbkit_library name sources libs)
	string(REPLACE " " ";" sources_list ${sources})
	add_library(${name} SHARED ${sources_list})
	if (NOT ${libs} STREQUAL "")
		string(REPLACE " " ";" libs_list ${libs})
		target_link_libraries(${name} ${libs_list})
	endif()
	install(TARGETS ${name} DESTINATION lib)
endfunction()

function(add_boost_test test_name)
	add_executable(${test_name} ${test_name}.cc)
	target_link_libraries(${test_name} boost_unit_test_framework ${ARGN})
	add_test(${test_name} ${test_name})
endfunction()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pipe -Wall -Werror -Wno-sign-compare -Woverloaded-virtual -fPIC -m64 -ggdb -fno-omit-frame-pointer -std=c++0x -Wno-deprecated-declarations")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-deprecated -Winit-self -fno-omit-frame-pointer -std=c++0x -fno-deduce-init-list -msse3 -Ileveldb/include -Wno-unused-but-set-variable -Wno-psabi -D__GXX_EXPERIMENTAL_CXX0X__=1")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -DBOOST_DISABLE_ASSERTS -DNDEBUG")

#CXXLINKFLAGS = -rdynamic $(foreach DIR,$(PWD)/$(BIN) $(PWD)/$(LIB) $(LOCAL_LIB_DIR),-L$(DIR) -Wl,--rpath-link,$(DIR)) -Wl,--rpath,\$$ORIGIN/../bin -Wl,--rpath,\$$ORIGIN/../lib -Wl,--copy-dt-needed-entries -Wl,--no-as-needed

include_directories("~/local/include")
include_directories("~/local/include/node")
include_directories("${PROJECT_SOURCE_DIR}/jml")
include_directories("${PROJECT_SOURCE_DIR}/soa")
include_directories("${PROJECT_SOURCE_DIR}/leveldb/include")
include_directories("${PROJECT_SOURCE_DIR}")

link_directories("~/local/lib")

#add_library(tinyxml2 SHARED tinyxml2/tinyxml2.cpp)
add_rtbkit_library(tinyxml2 "tinyxml2/tinyxml2.cpp" "dl")

add_subdirectory(googleurl)
add_subdirectory(jml)
add_subdirectory(leveldb)
add_subdirectory(rtbkit)
add_subdirectory(soa)
