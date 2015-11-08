add_library(sigslot SHARED
	slot.cc
	signal.cc
	slot_js.cc
	)
target_link_libraries(sigslot js arch)

#LIBSIGSLOT_JS_SOURCES := \
#	slot_node.cc
#
#LIBSIGSLOT_JS_LINK := \
#	sigslot
#
#$(eval $(call nodejs_addon,sigslot,$(LIBSIGSLOT_JS_SOURCES),$(LIBSIGSLOT_JS_LINK)))
#
#$(eval $(call include_sub_make,sigslot_testing,testing,sigslot_testing.mk))
