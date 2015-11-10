# create by lsm <lsm@skybility.com>
# cmake

cmake_minimum_required(VERSION 2.8)

project(zlog)
message(STATUS "path : ${CMAKE_FIND_ROOT_PATH}")

set(CMAKE_MODULE_PATH ${zlog_SOURCE_DIR}/cmake)

message(STATUS "platform : ${CMAKE_SYSTEM}")

add_definitions("-g -Wall -Wstrict-prototypes")
set(CMAKE_C_FLAGS "-std=c99 -pedantic -D_DEFAULT_SOURCE")
set(CMAKE_C_FLAGS_DEBUG "-ggdb3 -DDEBUG")
set(CMAKE_C_FLAGS_RELEASE "-O2")

if (WIN32)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DWINVER=0x0602 -D_WIN32_WINNT=0x0602 ")
endif()

if (WIN32)
    find_path(UNIXEM_INCLUDE_DIR
            NAMES
                unixem/unixem.h
            ONLY_CMAKE_FIND_ROOT_PATH
        )
    include_directories(${UNIXEM_INCLUDE_DIR})

    set (UNIXEM_LIBRARY ${UNIXEM_INCLUDE_DIR}/../lib)
    link_directories(${UNIXEM_LIBRARY})
    message (STATUS " UNIXEM_INCLUDE_DIR : ${UNIXEM_INCLUDE_DIR}")
    message (STATUS " UNIXEM_LIBRARY : ${UNIXEM_LIBRARY}")
endif()

cmake_policy(SET CMP0015 NEW)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${zlog_BINARY_DIR}/lib")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${zlog_BINARY_DIR}/lib")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${zlog_BINARY_DIR}/bin")

link_directories(${CMAKE_LIBRARY_OUTPUT_DIRECTORY})

add_subdirectory(src)
