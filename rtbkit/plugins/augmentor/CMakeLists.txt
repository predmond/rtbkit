add_library(augmentor_base SHARED augmentor_base.cc redis_augmentor.cc)
target_link_libraries(augmentor_base zmq rtb bid_request services redis agent_configuration)
#$(eval $(call include_sub_make,augmentor_testing,testing,augmentor_testing.mk))
