add_library(test_utils SHARED benchmarks.cc fixtures.cc threaded_test.cc)
target_link_libraries(test_utils arch utils boost_filesystem boost_thread)

add_library(variadic_hash variadic_hash.cc)
target_link_libraries(variadic_hash cityhash)

add_library(string_encryption string_encryption.cc)
target_link_libraries(string_encryption crypto++)

add_executable(string_encryption_keygen string_encryption_keygen.cc)
target_link_libraries(string_encryption_keygen string_encryption)

# CMAKE TODO
#ifeq ($(PYTHON_ENABLED),1)
#
#$(eval $(call library,py_util,py.cc,boost_python python$(PYTHON_VERSION)))
#$(eval $(call set_compile_option,py.cc,-I$(PYTHON_INCLUDE_PATH)))
#
#endif # PYTHON_ENABLED
#
#$(eval $(call include_sub_make,testing))
