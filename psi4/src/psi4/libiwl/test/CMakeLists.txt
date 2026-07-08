# Standalone round-trip exerciser for libiwl. Links the libiwl/libpsio/
# libpsi4util/liboptions/libciomr static archives plus a tiny stubs TU
# (test/stubs.cc) that supplies the runtime globals normally provided by
# core.cc / libdpd. This keeps the test self-contained without pulling the
# full libmints/Libint closure.
#
# Only the executable is defined here. psi4-core is configured as a separate
# ExternalProject with its own binary dir and never calls enable_testing(), so
# an add_test() in this scope would generate no CTestTestfile.cmake and would
# be invisible to the `ctest` that CI runs from the superbuild directory.
# Registration therefore lives in the superbuild, in tests/libiwl/.
add_executable(iwl_roundtrip_test.x iwl_roundtrip_test.cc stubs.cc)
target_link_libraries(iwl_roundtrip_test.x PRIVATE iwl psio psi4util options ciomr)
target_include_directories(iwl_roundtrip_test.x PRIVATE
    ${CMAKE_SOURCE_DIR}/src
    ${CMAKE_BINARY_DIR}/src
)
