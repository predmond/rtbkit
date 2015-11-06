add_library(db SHARED
        compact_size_types.cc
        nested_archive.cc
        portable_iarchive.cc
        portable_oarchive.cc)
target_link_libraries(db utils)

#$(eval $(call include_sub_make,db_testing,testing))
