esma_set_this ()

esma_add_library (${this}
  SRCS ${this}Mod.F90
  DEPENDENCIES Chem_Shared Chem_Base GMAO_mpeu MAPL_cfio_r4 MAPL)
target_include_directories (${this} PUBLIC ${INC_ESMF} ${INC_NETCDF})

esma_generate_gocart_code (${this} "-B\;-E\;-C\;-N\;GOCART")

#mapl_acg (${this} BRC_Registry.rc
#        IMPORT_SPECS EXPORT_SPECS INTERNAL_SPECS
#        GET_POINTERS DECLARE_POINTERS)

file (GLOB_RECURSE rc_files RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.rc)
foreach ( file ${rc_files} )
   get_filename_component( dir ${file} DIRECTORY )
   install( FILES ${file} DESTINATION etc/${dir} )
endforeach()
