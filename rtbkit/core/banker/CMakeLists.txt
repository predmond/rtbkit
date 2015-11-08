add_library(banker SHARED 
	account.cc
	banker.cc
	null_banker.cc
	slave_banker.cc
	master_banker.cc
	application_layer.cc
	)
target_link_libraries(banker types services redis monitor boost_program_options)

add_executable(banker_service_runner banker_service_runner.cc)
target_link_libraries(banker_service_runner banker boost_program_options)

add_library(gobanker SHARED go_account.cc local_banker.cc)

#$(eval $(call python_program,banker_backup,banker_backup.py))
#$(eval $(call python_program,banker_restore,banker_restore.py))

add_subdirectory(migration)
#$(eval $(call include_sub_make,banker_testing,testing,banker_testing.mk))
