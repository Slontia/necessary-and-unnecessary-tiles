cmake_minimum_required(VERSION 3.1)

project(shanten-number-calculator)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS_DEBUG "-O0 -Wall -g -DCHECK_HAND")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall")

add_custom_target(make_index_dw ALL
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    COMMAND ${CMAKE_COMMAND} -E tar zxvf ${CMAKE_CURRENT_SOURCE_DIR}/index_dw.hpp.tar.gz)

option(THREE_PLAYER "Three player mode" off)

if(THREE_PLAYER)
  add_definitions(-DTHREE_PLAYER)
endif()

include_directories(${CMAKE_CURRENT_BINARY_DIR})

add_library(calsht_dw SHARED calsht_dw.cpp)
add_dependencies(calsht_dw make_index_dw)

add_executable(mkind2 mkind2.cpp judwin.cpp)
add_executable(sample sample.cpp)

target_link_libraries(sample calsht_dw)
