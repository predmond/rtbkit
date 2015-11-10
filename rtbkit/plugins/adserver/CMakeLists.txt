add_library(adserver_connector SHARED
	adserver_connector.cc
	http_adserver_connector.cc
	)
target_link_libraries(adserver_connector
	zeromq boost_thread utils services rtb gc
	)

add_library(mock_adserver SHARED
	mock_adserver_connector.cc mock_win_source.cc mock_event_source.cc
	)
target_link_libraries(mock_adserver adserver_connector bid_test_utils)

add_library(standard_adserver SHARED
	standard_adserver_connector.cc standard_win_source.cc standard_event_source.cc
	)
target_link_libraries(standard_adserver
	adserver_connector bid_test_utils
	)

add_executable(adserver_runner adserver_runner.cc)
target_link_libraries(adserver_runner
	adserver_connector boost_program_options services
	)

add_subdirectory(testing)
