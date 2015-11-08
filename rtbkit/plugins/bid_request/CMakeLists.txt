add_library(mock_bid_request SHARED mock_bid_source.cc)
target_link_libraries(mock_bid_request bid_request bid_test_utils)

add_library(openrtb_bid_request_old SHARED openrtb_bid_request.cc)
target_link_libraries(openrtb_bid_request_old bid_request bid_test_utils openrtb)

add_library(fbx_bid_request SHARED fbx_bid_request.cc fbx_parsing.cc)
target_link_libraries(fbx_bid_request bid_request)

add_library(appnexus_bid_request SHARED appnexus_bid_request.cc appnexus_parsing.cc)
target_link_libraries(appnexus_bid_request bid_request openrtb)

add_library(openrtb_bid_request SHARED openrtb_bid_request_parser.cc openrtb_bid_source.cc)
target_link_libraries(openrtb_bid_request bid_request bid_test_utils openrtb)

#$(eval $(call include_sub_make,bid_request_testing,testing,bid_request_testing.mk))
