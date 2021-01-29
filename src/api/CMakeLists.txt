cmake_minimum_required(VERSION 3.13)

project(api
        VERSION 0.1
        DESCRIPTION "Homeberry API, provides the single point of access for users of the Homeberry system."
        LANGUAGES CXX)

# Configure required libraries
find_package(Boost REQUIRED COMPONENTS system thread log program_options chrono)
find_package(Threads REQUIRED)
find_package(cpprestsdk REQUIRED)

# Find the PI's64bit arch and add in as -arch x86_64 or equiv
set(CMAKE_CXX_FLAGS "-std=c++17 -DBOOST_LOG_DYN_LINK -Wno-deprecated-declarations")

add_executable(api src/main.cpp)

## Header search paths
set(HOMEBERRY_INCLUDE_DIR "./include")
message(HOMEBERRY " ${HOMEBERRY_INCLUDE_DIR}")
set(HEADER_SEARCH_PATHS ${HOMEBERRY_INCLUDE_DIR} ${Boost_INCLUDE_DIR} ${OPENSSL_INCLUDE_DIR})

##  Library search paths
set(OPENSSL_LIBS "${OPENSSL_LIBRARIES}")
set(LIBRARIES_SEARCH_PATHS ${OPENSSL_LIBS} ${Boost_LIBRARIES})

message(BOOST_LIBS " ${Boost_LIBRARIES}")
message(OPENSSL_LIBS " ${OPENSSL_LIBRARIES}")
message(LIBRARIES_SEARCH_PATHS " ${LIBRARIES_SEARCH_PATHS}")

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

include_directories(${HEADER_SEARCH_PATHS})
# Link Boost, OpenSSL and cpprestsdk
target_link_libraries(${PROJECT_NAME} PRIVATE ${LIBRARIES_SEARCH_PATHS} cpprestsdk::cpprest)