# What you will rename, when starting a real project:
# - MB_CPP_LIB_TEMPLATE_HEADER_ONLY
# - cpp-lib-template-header-only
# - mb.
# - mb::
# - mb/

cmake_minimum_required(VERSION 3.30...4.3)

project(
    mb.cpp-lib-template-header-only # CMake Project Name, which is also the name of the top-level
    # targets (e.g., library, executable, etc.).
    DESCRIPTION "C++ library template"
    LANGUAGES CXX
    VERSION 0.1.0
)

# [CMAKE.SKIP_TESTS]
option(
    MB_CPP_LIB_TEMPLATE_HEADER_ONLY_BUILD_TESTS
    "Enable building tests and test infrastructure. Default: ${PROJECT_IS_TOP_LEVEL}. Values: { ON, OFF }."
    ${PROJECT_IS_TOP_LEVEL}
)

# [CMAKE.SKIP_EXAMPLES]
option(
    MB_CPP_LIB_TEMPLATE_HEADER_ONLY_BUILD_EXAMPLES
    "Enable building examples. Default: ${PROJECT_IS_TOP_LEVEL}. Values: { ON, OFF }."
    ${PROJECT_IS_TOP_LEVEL}
)

include(devenv/cmake/install-library-config.cmake)

add_library(mb.cpp-lib-template-header-only INTERFACE)
add_library(
    mb::cpp-lib-template-header-only
    ALIAS mb.cpp-lib-template-header-only
)

target_sources(
    mb.cpp-lib-template-header-only
    PUBLIC FILE_SET HEADERS BASE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/include"
)

set_target_properties(
    mb.cpp-lib-template-header-only
    PROPERTIES VERIFY_INTERFACE_HEADER_SETS ON
)

add_subdirectory(include/mb/cpp-lib-template-header-only)

mb_install_library(mb.cpp-lib-template-header-only)

if(MB_CPP_LIB_TEMPLATE_HEADER_ONLY_BUILD_TESTS)
    enable_testing()
    add_subdirectory(src)
endif()

if(MB_CPP_LIB_TEMPLATE_HEADER_ONLY_BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()
