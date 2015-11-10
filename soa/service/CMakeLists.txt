add_library(opstats SHARED statsd_connector.cc carbon_connector.cc stat_aggregator.cc process_stats.cc)
target_link_libraries(opstats ACE arch utils boost_thread types)

add_library(zeromq SHARED socket_per_thread.cc zmq_utils.cc)
target_link_libraries(zeromq zmq)

add_library(runner_common SHARED runner_common.cc)

add_executable(runner_helper runner_helper.cc)
target_link_libraries(runner_helper runner_common arch)

add_library(services SHARED
	active_endpoint.cc
	async_event_source.cc
	async_writer_source.cc
	chunked_http_endpoint.cc
	connection_handler.cc
	endpoint.cc
	epoller.cc
	event_publisher.cc
	event_subscriber.cc
	http_client.cc
	http_client_v1.cc
	http_client_v2.cc
	http_endpoint.cc
	http_header.cc
	http_named_endpoint.cc
	http_parsers.cc
	http_rest_proxy.cc
	json_endpoint.cc
	logs.cc
	loop_monitor.cc
	message_loop.cc
	named_endpoint.cc
	nprobe.cc
	nsq_client.cc 
	nsq_event_handler.cc
	passive_endpoint.cc
	port_range_service.cc
	rest_proxy.cc
	rest_request_binding.cc
	rest_request_router.cc
	rest_service_endpoint.cc
	runner.cc
	service_base.cc
	sink.cc
	tcp_client.cc
	transport.cc
	xml_helpers.cc
	zmq_endpoint.cc
	zookeeper.cc
	zookeeper_configuration_service.cc
	)
target_link_libraries(services opstats curl curlpp boost_regex runner_common zeromq zookeeper_mt ACE arch utils jsoncpp boost_thread zmq types tinyxml2 boost_system value_description)
set_property(SOURCE runner.cc PROPERTY COMPILE_DEFINITIONS BIN="foobar")

#add_library(endpoint SHARED endpoint.cc)
#target_link_libraries(endpoint services)

add_library(cloud SHARED
	fs_utils.cc
	sftp.cc
	s3.cc
	sns.cc
	aws.cc
	sqs.cc
	)
target_link_libraries(cloud
	crypto++ curlpp utils arch types tinyxml2 services ssh2 boost_filesystem value_description)

add_library(redis SHARED redis.cc)
target_link_libraries(redis hiredis utils types boost_thread)

#$(eval $(call program,s3_transfer_cmd,cloud boost_program_options boost_filesystem utils))
#$(eval $(call program,s3tee,cloud boost_program_options utils))
#$(eval $(call program,s3cp,cloud boost_program_options utils))
#$(eval $(call program,s3_multipart_cmd,cloud boost_program_options utils))
#$(eval $(call program,syslog_trace,services))
#$(eval $(call program,s3cat,cloud boost_program_options utils))
#$(eval $(call program,sns_send,cloud boost_program_options utils))

#SERVICEDUMP_LINK = services boost_program_options

#$(eval $(call program,service_dump,$(SERVICEDUMP_LINK)))


#$(eval $(call include_sub_make,service_js,js,service_js.mk))
#$(eval $(call include_sub_make,service_testing,testing,service_testing.mk))
add_subdirectory(testing)
