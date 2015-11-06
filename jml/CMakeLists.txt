#HAS_EXCEPTION_HOOK := 1
#
## Fortran is required at this point so set it to gfortran (since make sets FC to f77 by default)
#FC := gfortran
#
#$(eval $(call include_sub_makes,math arch utils db algebra stats judy boosting python neural tsne))

#add_subdirectory(math)
add_subdirectory(arch)
add_subdirectory(utils)
add_subdirectory(db)
#add_subdirectory(algebra)
#add_subdirectory(stats)
#add_subdirectory(judy)
#add_subdirectory(boosting)
#add_subdirectory(python)
#add_subdirectory(neural)
#add_subdirectory(tsne)
