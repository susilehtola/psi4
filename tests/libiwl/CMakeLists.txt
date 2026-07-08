# C++ unit tests for libiwl.
#
# The executables are built inside the psi4-core ExternalProject, which has its
# own binary directory and does not call enable_testing(). Registration has to
# happen here, in the superbuild, because that is where `enable_testing()` runs
# (cmake/ConfigTesting.cmake) and where CI invokes `ctest`.
ExternalProject_Get_Property(psi4-core BINARY_DIR)

add_test(NAME libiwl-roundtrip
         COMMAND ${BINARY_DIR}/src/psi4/libiwl/test/iwl_roundtrip_test.x${CMAKE_EXECUTABLE_SUFFIX}
         WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})
set_tests_properties(libiwl-roundtrip PROPERTIES LABELS "psi;quicktests;libiwl")
