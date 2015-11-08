add_library(data_logger SHARED data_logger.cc)
target_link_libraries(data_logger
	ACE arch utils logger boost_thread zmq opstats services monitor
	)
