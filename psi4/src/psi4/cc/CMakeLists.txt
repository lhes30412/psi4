psi4_add_module(bin cc "")

# FIXME Remove once done
list(APPEND _Clang_debug_flags
  "-Wall"
  "-O0"
  "-g3"
  "-Wextra"
  "-Winit-self"
  "-Woverloaded-virtual"
  "-Wuninitialized"
  "-Wmissing-declarations"
  "-Wwrite-strings"
  "-Weffc++"
  "-Wdocumentation"
  "-Wno-sign-compare"
  "-m64"
  "-Qunused-arguments"
  "-fcolor-diagnostics"
  )
target_compile_options(cc
  PRIVATE
  $<$<AND:$<CXX_COMPILER_ID:Clang>,$<CONFIG:Debug>>:${_Clang_debug_flags}>
  )

list(APPEND _ccmodules
  ccdensity
  ccenergy
  cceom
  cchbar
  cclambda
  ccresponse
  cctriples
  )
foreach(dir_name IN LISTS _ccmodules)
  add_subdirectory(${dir_name})
endforeach ()
