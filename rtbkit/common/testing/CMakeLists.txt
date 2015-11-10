add_library(bid_test_utils SHARED exchange_source.cc)
target_link_libraries(bid_test_utils bid_request rtb)

add_library(bid_request_synth SHARED bid_request_synth.cc)
target_link_libraries(bid_request_synth arch utils jsoncpp)

add_boost_test(bid_request_synth_test bid_request_synth)
add_boost_test(currency_test bid_request)
add_boost_test(filter_test filter_registry)
add_boost_test(bids_test rtb)
