add_library(agent_configuration SHARED
	agent_config.cc
	blacklist.cc
	include_exclude.cc
	agent_configuration_listener.cc
	agent_configuration_service.cc
	latlonrad.cc
	fees.cc
	)
target_link_libraries(agent_configuration rtb zeromq boost_thread opstats gc services utils monitor)

add_executable(agent_configuration_service_runner agent_configuration_service_runner.cc)
target_link_libraries(agent_configuration_service_runner agent_configuration boost_program_options opstats)

#$(eval $(call include_sub_make,rtb_agent_configuration_testing,testing,rtb_agent_configuration_testing.mk))

