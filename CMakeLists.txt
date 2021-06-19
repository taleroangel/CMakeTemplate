#   PROJNAME - Ángel Talero
#   GitHub: @taleroangel

# Minimum required version of CMake
cmake_minimum_required(VERSION 3.20)

# Make sure project is not built in the root directory
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)
    message(FATAL_ERROR
    "Do not build in root directory, remove 'CMakeCache.txt' and re-build in 'build' directory")
endif()

# Project name and Description
project(
    "PROJNAME"
    VERSION 2.0.1
    DESCRIPTION "Brief CMake project Description"
    HOMEPAGE_URL "https://github.com/taleroangel"
    LANGUAGES CXX
    )

# Specify C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Configure file
configure_file(
    "${CMAKE_SOURCE_DIR}/include/CMakeConfig.h.in" "${CMAKE_SOURCE_DIR}/include/CMakeConfig.h"
)

# Append modules path
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/modules")

# Recursive source files
file(GLOB_RECURSE SRC_FILES "src/*.cpp")

# Add main executable and source files
add_executable(
    ${PROJECT_NAME} "${CMAKE_SOURCE_DIR}/src/${PROJECT_NAME}.cpp" ${SRC_FILES}
    )

# Include directory
target_include_directories(
    ${PROJECT_NAME} PUBLIC "${CMAKE_SOURCE_DIR}/include"
)