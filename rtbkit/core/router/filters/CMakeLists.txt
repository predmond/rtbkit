add_library(static_filters
	static_filters.cc
        creative_filters.cc
	)
target_link_libraries(static_filters 
	arch utils filter_registry agent_configuration rtb
	)

#$(eval $(call include_sub_make,filters_test,testing,filters_test.mk))
