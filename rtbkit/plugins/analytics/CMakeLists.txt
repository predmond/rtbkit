add_library(analytics SHARED analytics_endpoint.cc)
target_link_libraries(analytics services)

add_executable(analytics_runner analytics_runner.cc)
target_link_libraries(analytics_runner analytics boost_program_options)

#$(eval $(call include_sub_make,analytics_testing,testing,analytics_testing.mk))
