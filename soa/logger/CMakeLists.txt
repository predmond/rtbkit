add_library(logger SHARED
	logger.cc remote_output.cc remote_input.cc
	file_output.cc publish_output.cc
	filter.cc json_filter.cc stats_output.cc callback_output.cc
	rotating_output.cc cloud_output.cc compressor.cc compressing_output.cc
	multi_output.cc
	)
target_link_libraries(logger 
	ACE arch utils boost_thread boost_regex zeromq services lzma boost_filesystem opstats cloud gc)

#$(eval $(call nodejs_addon,logger,logger_js.cc filter_js.cc,logger js sigslot))

add_library(log_metrics SHARED
	kvp_logger_interface.cc easy_kvp_logger.cc logger_metrics_interface.cc
	logger_metrics_term.cc
	)
target_link_libraries(log_metrics mongoclient boost_filesystem boost_program_options types)

add_subdirectory(js)

#$(eval $(call include_sub_make,logger_testing,testing,logger_testing.mk))
