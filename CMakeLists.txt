cmake_minimum_required(VERSION 3.16)
project(grf C)

set(CMAKE_C_STANDARD 99)

add_library(grf STATIC)

target_include_directories(grf PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")

find_package(ZLIB REQUIRED)
#include_directories(ZLIB_INCLUDE_DIRS)

set_target_properties(grf PROPERTIES POSITION_INDEPENDENT_CODE ON)

target_compile_definitions(grf PUBLIC GRF_STATIC)
target_sources(grf PRIVATE src/grf.c src/grfcrypt.c src/grfsupport.c src/rgz.c)
target_link_libraries(grf PUBLIC ZLIB::ZLIB)