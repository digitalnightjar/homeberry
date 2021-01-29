#==========# CMake Min Req'd #==========#
cmake_minimum_required(VERSION 3.13 FATAL_ERROR)

#==========# Project Information #==========#
project(homeberry_api_unit LANGUAGES CXX)
message("/t###### homeberry_unit_tests ######")

file(GLOB SRCS *.cpp)

add_executable(homeberry_api_unit ${SRCS})

enable_testing()

target_link_libraries(homeberry_api_unit
    libgtest
    libgmock
)

add_test(NAME Test COMMAND homeberry_api_unit)

install(TARGETS homeberry_api_unit DESTINATION bin)


#==========# Options #==========#
#option(ENABLE_TEST_COVERAGE "Enable test coverage" OFF)
#option(TEST_INSTALLED_VERSION "Test the version found by find_package" OFF)

#==========# Import Tools #==========#
#include(../cmake/tools.cmake)

#==========# Dependencies #==========#
#include(../cmake/CPM.cmake)
#find_package(PkgConfig)
#pkg_check_modules(GTEST REQUIRED gtest>=1.7.0)
#pkg_check_modules(GMOCK REQUIRED gmock>=1.7.0)

#include_directories(
#    ${GTEST_INCLUDE_DIRS}
#    ${GMOCK_INCLUDE_DIRS}
#)

# Enable Testing
#SET(CMAKE_CXX_FLAGS -pthread)
#enable_testing()

#include_directories(${GTEST_INCLUDE_DIRS} ${GMOCK_INCLUDE_DIRS})

#add_executable(homeberry_unit_tests main.cpp initial_test.cpp)

#target_link_libraries(homeberry_unit_tests ${GTEST_LIBRARIES} )

#add_test(NAME Test COMMAND homeberry_unit_tests)

#if(TEST_INSTALLED_VERSION)
#  find_package(homeberry REQUIRED)
#else()
#  CPMAddPackage(NAME homeberry SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/..)
#endif()

# Add the Test Executables
#add_executable(test_pimonitor PIMONITOR_TEST_SOURCE)
#add_executable(test_api API_TEST_SOURCE)

# Link GoogleTest
#target_link_libraries(test_pimonitor PRIVATE )

# Register the tests so that ctest and make test will run them.
#add_test(NAME unit_test_pimonitor COMMAND test_pimonitor)
#add_test(NAME unit_test_api COMMAND test_api)
#add_test(NAME unit_test_auth COMMAND test_auth)
