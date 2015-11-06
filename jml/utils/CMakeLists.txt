add_library(utils SHARED
        environment.cc
        exception_ptr.cc
        file_functions.cc
        filter_streams.cc
        string_functions.cc
        parse_context.cc
	configuration.cc
	csv.cc
	exc_check.cc
	exc_assert.cc
	hex_dump.cc
	lzma.cc
	xxhash.c
	lz4.c
	lz4hc.c
	floating_point.cc
	json_parsing.cc
	rng.cc
	hash.cc
	abort.cc)
target_link_libraries(utils ACE arch boost_iostreams lzma boost_thread cryptopp)

add_executable(lz4cli lz4cli.c lz4.c lz4hc.c xxhash.c)

add_library(worker_task SHARED worker_task.cc)
target_link_libraries(worker_task ACE arch pthread)

#$(eval $(call include_sub_make,utils_testing,testing))
