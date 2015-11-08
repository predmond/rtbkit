add_library(bid_request SHARED 
	bid_request.cc
	segments.cc
	json_holder.cc
	currency.cc
	expand_variable.cc)
target_link_libraries(bid_request types boost_regex db openrtb value_description)

add_library(rtb SHARED
	auction.cc
	augmentation.cc
	account_key.cc
	bids.cc
	auction_events.cc
	exchange_connector.cc
	bidder_interface.cc
	win_cost_model.cc
	post_auction_proxy.cc
	analytics_publisher.cc)
target_link_libraries(rtb
	ACE arch utils jsoncpp boost_thread
	#endpoint
	boost_regex zmq opstats bid_request)

add_library(filter_registry SHARED filter.cc)
target_link_libraries(filter_registry arch utils rtb)

add_subdirectory(testing)
