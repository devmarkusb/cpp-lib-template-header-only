find_package(GTest REQUIRED)

add_executable(mb.cpp-lib-template-header-only.test)
target_sources(mb.cpp-lib-template-header-only.test PRIVATE cpp-lib-template-header-only.test.cpp)
target_link_libraries(
    mb.cpp-lib-template-header-only.test
    PRIVATE mb::cpp-lib-template-header-only GTest::gtest GTest::gtest_main
)

include(GoogleTest)
gtest_discover_tests(mb.cpp-lib-template-header-only.test)
