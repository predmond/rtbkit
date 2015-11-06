add_library(arch SHARED
        simd_vector.cc
        demangle.cc
	tick_counter.cc
	cpuid.cc
	simd.cc
	exception.cc
	exception_handler.cc
	backtrace.cc
	format.cc
	fslock.cc
	gpgpu.cc
	environment_static.cc
	cpu_info.cc
	vm.cc
	info.cc
	rtti_utils.cc
	rt.cc)
target_link_libraries(arch ACE dl boost_system)

# CMAKE TODO
#ifneq ($(BOOST_VERSION),42)
#LIBARCH_LINK += boost_system
#endif
#$(eval $(call set_single_compile_option,simd_vector.cc,-funsafe-loop-optimizations -Wunsafe-loop-optimizations))

add_library(exception_hook exception_hook.cc)
target_link_libraries(exception_hook arch dl)

add_library(node_exception_tracing node_exception_tracing.cc)
target_link_libraries(node_exception_tracing arch dl)

#ifeq ($(CUDA_ENABLED),1)
#
#LIBARCH_CUDA_SOURCES 	:= cuda.cc
#LIBARCH_CUDA_LINK 	:= arch OcelotIr OcelotParser OcelotExecutive OcelotTrace OcelotAnalysis hydrazine
#
#$(eval $(call library,arch_cuda,$(LIBARCH_CUDA_SOURCES),$(LIBARCH_CUDA_LINK)))
#
#endif # CUDA_ENABLED
#
#
#ifeq ($(CAL_ENABLED),1)
#
#LIBARCH_CAL_SOURCES 	:= cal.cc
#LIBARCH_CAL_LINK 	:= arch amd
#
#$(eval $(call library,arch_cal,$(LIBARCH_CAL_SOURCES),$(LIBARCH_CAL_LINK)))
#
#endif # CAL_ENABLED
#
#$(eval $(call include_sub_make,arch_testing,testing))
