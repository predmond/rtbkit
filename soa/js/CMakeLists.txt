add_library(js SHARED
	js_wrapped.cc
	js_value.cc
	js_utils.cc
	js_registry.cc
	js_call.cc
	)
target_link_libraries(js arch utils types)
#$(eval $(call include_sub_make,js_testing,testing,js_testing.mk))
