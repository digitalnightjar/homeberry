cmake_minimum_required(VERSION 3.13 FATAL_ERROR)

project(homeberry
        VERSION 0.1
        DESCRIPTION "Smart Home Hub for Raspberry PI, providing a single API/Access point to control ESP8266 gadgets."
        LANGUAGES CXX)

#Options: Things you can set via cmdline args to cmake (e.g. -DENABLE_LTO=[ON|OFF)
option(ENABLE_WARNINGS_SETTINGS "Allow target_set_warnings to add flags and defines.
                                 Set this to OFF if you want to provide your own warnings parameters." ON)                                 
option(ENABLE_LTO "Enable link time optimization" ON)
option(ENABLE_DOCTESTS "Include tests in the library. Setting this to OFF will remove all doctest related code.
                        Tests in tests/*.cpp will still be enabled." ON)

# TODO: Make this more generic
set ( CMAKE_PREFIX_PATH /usr/lib/arm-linux-gnueabihf/cmake )
# Include stuff. No change needed.
#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
#include(ConfigSafeGuards)
#include(Colors)
#include(CTest)
#include(Doctest)
#include(Documentation)
#include(LTO)
#include(Misc)
#include(Warnings)

# Check for LTO support.
#find_lto(CXX)

if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    # Set global flags here (should only be things like -W flags / CXX Standard)
    set(CXX_STANDARD 17)
    set(CXX_STANDARD_REQUIRED ON)
    # Ensure -std=c++xx instead of -std=g++xx
    set(CMAKE_CXX_EXTENSIONS OFF)
endif()

# PI Monitor Library provides resource information for the host. 
add_subdirectory(src/pimonitor)
# Auth provides some basic user authentication (TODO)
add_subdirectory(src/auth)
# API is an executable that provides the REST API for the service.
add_subdirectory(src/api)

#if((CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME OR HOMEBERRY_TESTING) AND BUILD_TESTS)
    add_subdirectory(tests)
#endif()