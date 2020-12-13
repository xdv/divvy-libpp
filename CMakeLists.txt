
cmake_minimum_required(VERSION 3.9)
project(divvy-libppdemo)

#[===========================================[
  this pulls-in the divvyd source code via
  git submodule. This demo exe depends on the
  xdvl_core library which is defined by the
  divvyd project.
#]===========================================]
if (MSVC)
  #[=======================================[
    HACK to patch a one-line windows-only
    bug in divvyd CMakeLists.txt. This can
    be removed once divvyd 1.2 is available
    and we update the submodule
  #]=======================================]
  execute_process( COMMAND powershell -Command
     "(Get-Content extras/divvyd/CMakeLists.txt) \
     -replace '^exclude_if_included\\s+\\(rocksdb\\)', '##' \
     | Set-Content extras/divvyd/CMakeLists.txt"
     WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
  )
endif ()
add_subdirectory(extras/divvyd)

add_executable(divvylibppdemo src/test/divvy-libpp_demo.cpp)
target_link_libraries (divvylibppdemo Divvy::xdvl_core)
