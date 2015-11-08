add_library(post_auction SHARED
        simple_event_matcher.cc
	sharded_event_matcher.cc
	events.cc
	finished_info.cc
	post_auction_service.cc
	)
target_link_libraries(post_auction 
	agent_configuration zeromq boost_thread logger opstats leveldb services banker
	gobanker
	rtb
	)

add_executable(post_auction_runner post_auction_runner.cc)
target_link_libraries(post_auction_runner
	post_auction services banker gobanker boost_program_options)

#$(eval $(call include_sub_make,post_auction_testing,testing,testing.mk))
