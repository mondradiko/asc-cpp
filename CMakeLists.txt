cmake_minimum_required(VERSION 3.9)

project(asc-cpp VERSION 0.0.0)

# TODO(marceline-cramer) Use system binaryen over the git submodule if available?
set(BUILD_STATIC_LIB ON)
add_subdirectory(binaryen/)

find_library(wasmtime wasmtime)

set(ASC_CPP_SRC
  src/main.c
  src/asc-cpp-binaryen.h
  src/asc-cpp-wasmtime.h
)

set(ASC_CPP_BINARYEN_SRC
  src/asc-cpp-binaryen.cpp
  src/asc-cpp-binaryen.h
)

set(ASC_CPP_WASMTIME_SRC
  src/asc-cpp-wasmtime.cpp
  src/asc-cpp-wasmtime.h
)

add_library(asc-cpp-binaryen STATIC ${ASC_CPP_BINARYEN_SRC})
add_library(asc-cpp-wasmtime STATIC ${ASC_CPP_WASMTIME_SRC})
add_executable(asc-cpp-test ${ASC_CPP_SRC})

file(COPY src/start.wasm DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

target_include_directories(asc-cpp-binaryen PUBLIC binaryen/src/)
target_include_directories(asc-cpp-wasmtime PUBLIC wasm-c-api/include/)

target_link_libraries(asc-cpp-binaryen PRIVATE binaryen pthread)
target_link_libraries(asc-cpp-wasmtime PRIVATE wasmtime)
target_link_libraries(asc-cpp-test PUBLIC asc-cpp-binaryen asc-cpp-wasmtime)
