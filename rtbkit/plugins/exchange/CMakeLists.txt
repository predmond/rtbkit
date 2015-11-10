add_rtbkit_library(exchange
	"http_exchange_connector.cc http_auction_handler.cc"
	"zeromq boost_thread utils services rtb bid_request")
#add_library(exchange SHARED
#	http_exchange_connector.cc
#	http_auction_handler.cc
#	)
#target_link_libraries(exchange
#	zeromq boost_thread utils services rtb bid_request
#	)

add_rtbkit_library(openrtb_exchange
	"openrtb_exchange_connector.cc"
	"exchange bid_test_utils openrtb_bid_request")
#add_library(openrtb_exchange SHARED openrtb_exchange_connector)
#target_link_libraries(openrtb_exchange exchange bid_test_utils openrtb_bid_request)

add_library(rubicon_exchange SHARED rubicon_exchange_connector)
target_link_libraries(rubicon_exchange openrtb_exchange)

add_library(mopub_exchange SHARED mopub_exchange_connector)
target_link_libraries(mopub_exchange openrtb_exchange)

add_library(smaato_exchange SHARED smaato_exchange_connector)
target_link_libraries(smaato_exchange openrtb_exchange)

add_library(bidswitch_exchange SHARED bidswitch_exchange_connector)
target_link_libraries(bidswitch_exchange openrtb_exchange)

add_library(nexage_exchange SHARED nexage_exchange_connector)
target_link_libraries(nexage_exchange openrtb_exchange)

add_library(appnexus_exchange SHARED appnexus_exchange_connector)
target_link_libraries(appnexus_exchange exchange bid_test_utils appnexus_bid_request)

add_library(gumgum_exchange SHARED gumgum_exchange_connector)
target_link_libraries(gumgum_exchange exchange bid_test_utils openrtb_bid_request)

add_library(fbx_exchange SHARED fbx_exchange_connector)
target_link_libraries(fbx_exchange exchange bid_test_utils fbx_bid_request)

#add_library(adx_exchange SHARED realtime-bidding.proto adx_exchange_connector)
#target_link_libraries(adx_exchange exchange protobuf)

add_library(rtbkit_exchange SHARED rtbkit_exchange_connector)
target_link_libraries(rtbkit_exchange openrtb_exchange)

add_library(casale_exchange SHARED casale_exchange_connector)
target_link_libraries(casale_exchange openrtb_exchange)

add_library(spotx_exchange SHARED spotx_exchange_connector)
target_link_libraries(spotx_exchange openrtb_exchange)

#$(eval $(call include_sub_make,exchange_testing,testing,exchange_testing.mk))
