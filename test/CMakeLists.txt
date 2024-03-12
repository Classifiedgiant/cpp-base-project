project(test_target)

find_package(Catch2 3 REQUIRED)

add_executable(test_target dummy.test.cpp)

target_include_directories(test_target PRIVATE ../src)

target_link_libraries(test_target PRIVATE Catch2::Catch2WithMain)

include(CTest)
include(Catch)
catch_discover_tests(test_target)

add_custom_command(TARGET test_target
                   POST_BUILD
                   COMMAND ctest -C $<CONFIGURATION> --output-on-failure)