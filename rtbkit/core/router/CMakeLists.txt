add_subdirectory(filters)

add_library(rtb_router SHARED
	augmentation_loop.cc
	router.cc
	router_types.cc
	router_stack.cc
	filter_pool.cc
	)
target_link_libraries(rtb_router
	rtb zeromq boost_thread logger opstats crypto++ leveldb gc services redis
	banker gobanker agent_configuration monitor monitor_service post_auction
	static_filters openrtb
	)

add_executable(router_runner router_runner.cc)
target_link_libraries(router_runner rtb_router boost_program_options)

#$(eval $(call include_sub_make,rtb_router_testing,testing,rtb_router_testing.mk))
