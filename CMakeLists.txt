cmake_minimum_required(VERSION 3.10.0)
project(Kaleidoscope VERSION 0.1.0 LANGUAGES CXX C)

set(LLVM_DIR /usr/lib/llvm-18/lib/cmake/llvm/)
find_package(LLVM REQUIRED CONFIG)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")

include_directories(${LLVM_INCLUDE_DIRS})

add_executable(Kaleidoscope src/main.cpp include/KaleidoscopeJIT.h)
target_link_options(Kaleidoscope PRIVATE -Xlinker --export-dynamic)
add_executable(Chapter3 src/ch3.cpp)
add_executable(Chapter8 src/ch8/ch8.cpp)
target_link_options(Chapter8 PRIVATE -Xlinker --export-dynamic)

target_link_libraries(Kaleidoscope LLVM)
target_link_libraries(Chapter3 LLVM)
target_link_libraries(Chapter8 LLVM)

