cmake_minimum_required(VERSION 3.9)

project(asc-cpp VERSION 0.0.0)

set(BUILD_STATIC_LIB ON)
add_subdirectory(binaryen/)
include_directories(binaryen/src/)

set(ASC_CPP_SRC
  src/main.c
)

add_executable(asc-cpp-test ${ASC_CPP_SRC})
target_link_libraries(asc-cpp-test PUBLIC binaryen pthread)
