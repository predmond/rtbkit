add_library(openrtb SHARED openrtb_parsing.cc openrtb.cc)
target_link_libraries(openrtb value_description)
install(TARGETS openrtb DESTINATION bin)
