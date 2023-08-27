cmake_minimum_required(VERSION 3.16)
project(grf C)

option(GRF_BUILD_STATIC_LIB "Build the static library" OFF)

if (${GRF_BUILD_STATIC_LIBS})
	set(GRF_LIB_TYPE STATIC)
else ()
	set(GRF_LIB_TYPE SHARED)
endif ()

set(CMAKE_C_STANDARD 99)

find_package(ZLIB REQUIRED)

add_library(grf ${GRF_LIB_TYPE}
	src/grf.c
	src/grfcrypt.c
	src/grfsupport.c
	src/rgz.c
)

target_include_directories(grf PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
set_property(TARGET grf PROPERTY POSITION_INDEPENDENT_CODE ON)

target_link_libraries(grf PUBLIC ZLIB::ZLIB)
