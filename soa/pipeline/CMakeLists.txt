add_library(pipeline SHARED code.cc)
target_link_libraries(pipeline value_description services)
#$(eval $(call include_sub_make,pipeline_testing,testing,pipeline_testing.mk))
