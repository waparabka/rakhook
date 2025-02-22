cmake_minimum_required(VERSION 3.0)

project(RakHook VERSION 1.0 LANGUAGES CXX C)

if (CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    set(RAKHOOK_MASTER_PROJECT ON)
endif ()

option(RAKHOOK_INSTALL "Install targets" ${RAKHOOK_MASTER_PROJECT})

add_subdirectory(source)
