add_library(bidding_agent SHARED bidding_agent.cc)
target_link_libraries(bidding_agent
	ACE arch utils jsoncpp boost_thread zmq opstats bid_request services
	)
