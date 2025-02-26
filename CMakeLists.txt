cmake_minimum_required(VERSION 3.10)
project(MetaNN
    LANGUAGES CXX
    VERSION 0.2.0
)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -O0 -Wall")
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2 -Wall")
endif()

add_subdirectory(MetaNN)

option(BUILD_TESTING "Build the testing." ON)

if(BUILD_TESTING)
    add_subdirectory(Tests)
endif()