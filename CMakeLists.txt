cmake_minimum_required(VERSION 2.6)
project(RTBKit)

enable_testing()

include(ExternalProject)

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


#install_node:
#	if [ $(NODEJS_ENABLED) = 1 ]; \
#	then \
#		echo "node js enabled" && \
#		JOBS=$(JOBS) cd node && \
#		./recoset_build_node.sh;\
#	else \
#		echo "node js disabled"; \
#	fi
#
#install_boost:
#	if [ ! -f boost_1_57_0/b2 ] ; then cd boost_1_57_0 && ./bootstrap.sh --prefix=$(TARGET) ; fi
#	cd boost_1_57_0 && ./bjam include=/usr/lib && ./b2 -j$(JOBS) variant=release link=shared threading=multi runtime-link=shared toolset=gcc --without=graph --without-graph_parallel --without-mpi install
#
#clean_boost:
#	cd boost_1_57_0 && rm -rf ./b2 ./bin.v2 ./bjam ./bootstrap.log ./project-config.jam ./tools/build/v2/engine/bootstrap/ ./tools/build/v2/engine/bin.linuxx86_64/
#
#install_userspacercu:
#	cd userspace-rcu/ && ./bootstrap && ./configure --prefix=$(TARGET) && make install
#
#install_hiredis:
#	cd hiredis && PREFIX=$(TARGET) LIBRARY_PATH=lib make install

ExternalProject_Add(
	external_snappy
	GIT_REPOSITORY https://github.com/mikeburkat/snappy.git
	GIT_TAG 1ff9be9b8fafc8528ca9e055646f5932aa5db9c4
	BUILD_IN_SOURCE 1
	CONFIGURE_COMMAND ./autogen.sh && ./configure --prefix=${CMAKE_INSTALL_PREFIX}
	BUILD_COMMAND make
	INSTALL_COMMAND make install
	)

ExternalProject_Add(
	external_protobuf
	GIT_REPOSITORY https://github.com/datacratic/protobuf.git
	GIT_TAG 3a0ac8d73e8afb46ce5f7082f5304fe9492b8948
	BUILD_IN_SOURCE 1
	CONFIGURE_COMMAND ./autogen.sh && ./configure --prefix=${CMAKE_INSTALL_PREFIX}
	BUILD_COMMAND make
	INSTALL_COMMAND make install
	)

#DISABLE_SSE42 ?= 0
#ifneq ($(DISABLE_SSE42),0)
#CITYHASH_CXXFLAGS := -mno-sse4.2
#else
#CITYHASH_CONFIGURE_FLAGS := --enable-sse4.2
#endif
#
#install_cityhash:
#	cd cityhash && ./configure $(CITYHASH_CONFIGURE_FLAGS) --prefix $(TARGET) && make all check CXXFLAGS="-g -O3 $(CITYHASH_CXXFLAGS)" && make install

ExternalProject_Add(
	external_zeromq
	GIT_REPOSITORY https://github.com/datacratic/zeromq3-x.git
	GIT_TAG b1d325f485cdffbb914d9facb1f5af588b5a8112
	BUILD_IN_SOURCE 1
	CONFIGURE_COMMAND ./autogen.sh && ./configure --prefix=${CMAKE_INSTALL_PREFIX}
	BUILD_COMMAND make
	INSTALL_COMMAND make install
	)

ExternalProject_Add(
	external_libssh2
	GIT_REPOSITORY https://github.com/datacratic/libssh2.git
	GIT_TAG ed89a4885fb3189f5189cdb4a905c4e9cb8a7a46
	BUILD_IN_SOURCE 1
	CONFIGURE_COMMAND ./buildconf && ./configure --prefix=${CMAKE_INSTALL_PREFIX}
	BUILD_COMMAND make
	INSTALL_COMMAND make install
	)
#
#install_libssh2:
#	cd libssh2 && ./buildconf && ./configure --prefix $(TARGET) && make -j$(JOBS) -k && make install
#
#install_libcurl:
#	cd curl && ./buildconf && ./configure --prefix $(TARGET) --with-libssh2=$(TARGET) && make -j$(JOBS) -k && make install
#
#install_curlpp:
#	cd curlpp && ./autogen.sh && CXX="ccache g++" CXXFLAGS="-I$(TARGET)/include" CFLAGS="-I$(TARGET)/include" CC="ccache gcc" ./configure --prefix $(TARGET) --with-curl=$(TARGET) --with-boost=$(TARGET)/ && CXX="ccache g++" CC="ccache gcc" make -j$(JOBS) -k && make install
#	rm -f $(TARGET)/include/curlpp/config.win32.h
#	cp curlpp/include/curlpp/config.h $(TARGET)/include/curlpp/config.h
#	echo '#include "curlpp/config.h"' > $(TARGET)/include/curlpp/internal/global.h

ExternalProject_Add(
	external_zookeeper
	GIT_REPOSITORY https://github.com/apache/zookeeper.git
	GIT_TAG 26e8dd6e90726997a37965ef469e37a96ef7085f
	BUILD_IN_SOURCE 1
	CONFIGURE_COMMAND JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64/ ant compile &&
		cd src/c &&
		autoreconf -if &&
		./configure --prefix ${CMAKE_INSTALL_PREFIX}
	BUILD_COMMAND cd src/c && make -k
	INSTALL_COMMAND cd src/c && make -k install
	)

ExternalProject_Add(
	external_redis
	GIT_REPOSITORY https://github.com/datacratic/redis.git
	GIT_TAG 10323dc5feb2adc10c4d62c7d667fd45923d6a57
	BUILD_IN_SOURCE 1
	CONFIGURE_COMMAND ""
	BUILD_COMMAND make PREFIX=${CMAKE_INSTALL_PREFIX}
	INSTALL_COMMAND make PREFIX=${CMAKE_INSTALL_PREFIX} install
	)

ExternalProject_Add(
	external_cairomm
	GIT_REPOSITORY git://git.cairographics.org/git/cairomm
	GIT_TAG 174fe4c
	BUILD_IN_SOURCE 1
	CONFIGURE_COMMAND ./autogen.sh && ./configure --prefix=${CMAKE_INSTALL_PREFIX}
	BUILD_COMMAND make
	INSTALL_COMMAND make install
	)



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
