# Standalone round-trip exerciser for libpsio. Links the libpsio/libpsi4util/
# liboptions/libciomr static archives plus a tiny stubs TU (test/stubs.cc) for
# the runtime globals normally provided by core.cc, so the test is
# self-contained (no python, no libdpd).
#
# Only the executable is defined here. psi4-core is configured as a separate
# ExternalProject with its own binary dir and never calls enable_testing(), so
# an add_test() in this scope would generate no CTestTestfile.cmake and would
# be invisible to the `ctest` that CI runs from the superbuild directory.
# Registration therefore lives in the superbuild, in tests/libpsio/.
add_executable(psio_roundtrip_test.x psio_roundtrip_test.cc stubs.cc)
target_link_libraries(psio_roundtrip_test.x PRIVATE psio psi4util options ciomr)
target_include_directories(psio_roundtrip_test.x PRIVATE
    ${CMAKE_SOURCE_DIR}/src
    ${CMAKE_BINARY_DIR}/src
)
