cmake_minimum_required(VERSION 2.8)

project("libconsole")

add_library("libconsole_c" STATIC "console.h" "console.c")
add_library("libconsole_cpp" INTERFACE)

target_include_directories("libconsole_c" INTERFACE ${libconsole_SOURCE_DIR})
target_include_directories("libconsole_cpp" INTERFACE ${libconsole_SOURCE_DIR})
target_link_libraries("libconsole_cpp" INTERFACE "libconsole_c")

option(LIBCONSOLE_BUILD_DEMOS "Build the demos for libconsole" OFF)

if(LIBCONSOLE_BUILD_DEMOS)
	add_executable("demo_c" "demo.c")
	target_link_libraries("demo_c" PRIVATE "libconsole_c")
	add_executable("demo_cpp" "demo2.cpp")
	target_link_libraries("demo_cpp" PRIVATE "libconsole_cpp")
endif()