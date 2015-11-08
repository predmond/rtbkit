add_library(redis_migration SHARED
	redis_migration.cc
	redis_old_types.cc
	redis_rollback.cc
	redis_utils.cc
	)
target_link_libraries(redis_migration banker redis)

add_executable(redis_migrate redis_migrate.cc)
target_link_libraries(redis_migrate redis_migration boost_program_options)
