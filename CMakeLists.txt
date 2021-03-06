#   PROJNAME - Ángel Talero
#   GitHub: @taleroangel

# Minimum required version of CMake
cmake_minimum_required(VERSION 3.15)

# Make sure project is not built in the root directory
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)
    message(FATAL_ERROR
    "Do not build in root directory, remove 'CMakeCache.txt' and re-build in 'build' directory")
endif()

# Project name and Description
project(
    "PROJNAME"
    VERSION 0.1.0
    DESCRIPTION "Brief CMake project Description"
    HOMEPAGE_URL "https://github.com/taleroangel"
    LANGUAGES CXX
    )

# Specify C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Append ./cmake directory to our include paths for the find_package scripts
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

# Configure file
configure_file(
    "${CMAKE_SOURCE_DIR}/include/cmake_config.h.in" "${CMAKE_SOURCE_DIR}/include/cmake_config.h"
)

# Append sources
file(GLOB_RECURSE HEADERS CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/include/*.h")
file(GLOB_RECURSE HEADERS CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/include/*.hpp")
file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/source/*.cpp")

# Add main executable and source files
add_executable(
    ${PROJECT_NAME} "${CMAKE_SOURCE_DIR}/source/main.cpp"
)
   
# Add sources
target_sources(${PROJECT_NAME} PRIVATE ${SOURCES})

# Include directory
target_include_directories(
  ${PROJECT_NAME} PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
)
