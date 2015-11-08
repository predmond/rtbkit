add_library(gc SHARED gc_lock.cc)
target_link_libraries(gc arch utils urcu)
#$(eval $(call include_sub_make,gc_testing,testing,gc_testing.mk))
