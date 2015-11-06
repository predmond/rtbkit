add_library(types SHARED
	date.cc
	localdate.cc
	string.cc
	id.cc
	url.cc
	periodic_utils.cc
	csiphash.c)
target_link_libraries(types boost_regex boost_date_time jsoncpp ACE db googleurl cityhash utils)
# CMAKE TODO
set_property(SOURCE localdate.cc PROPERTY COMPILE_DEFINITIONS LIB="foobar")
#$(eval $(call set_compile_option,localdate.cc,-DLIB=\"$(LIB)\"))
#
#ifneq ($(PREMAKE),1)
#$(LIB)/libtypes.so: $(LIB)/date_timezone_spec.csv
#
#$(LIB)/date_timezone_spec.csv: $(CWD)/date_timezone_spec.csv
#	@echo "           $(COLOR_CYAN)[COPY]$(COLOR_RESET) $< -> $@"
#	@/bin/cp -f $< $@
#endif

add_library(value_description SHARED
	value_description.cc
	json_parsing.cc
	json_printing.cc
	periodic_utils_value_descriptions.cc)
target_link_libraries(value_description arch types)
