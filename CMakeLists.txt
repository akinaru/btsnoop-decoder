cmake_minimum_required (VERSION 2.6)

project(btsnoop-decoder)

if(UNIX)
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -m32 -Wall -std=c++11")
endif()

set(LIBRARY_OUTPUT_PATH lib/${CMAKE_BUILD_TYPE})

set(EXECUTABLE_OUTPUT_PATH bin/${CMAKE_BUILD_TYPE})

include_directories(
    include
    test/include
)

file(
        GLOB_RECURSE
        source_files
        src/*
        include/*
)

add_library(
        btsnoop_static
        STATIC
        ${source_files}
)

add_library(
        btsnoop
        SHARED
        ${source_files}
)

file(
        GLOB_RECURSE
        source_test_files
        test/src/*
        test/include/*
)

add_executable(
        btsnoop-test
        ${source_test_files}
)

target_link_libraries(
        btsnoop-test
        btsnoop
        pthread
)