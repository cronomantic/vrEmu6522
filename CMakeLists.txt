cmake_minimum_required(VERSION 3.12)


set(CMAKE_C_STANDARD 11)

option(BUILD_SHARED_LIBS "Build using shared libraries" ON)

project(vrEmu6522)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/)

if (NOT BUILD_SHARED_LIBS)
 add_definitions(-DVR_6522_EMU_STATIC)
endif()

if(MSVC)
  add_compile_options(/W4 /WX)
  add_compile_options(/arch:AVX2 /Ox)
else()
  add_compile_options(-Wall -Wextra -Wpedantic -Werror)
  if (UNIX)
    add_compile_options(-march=native)
  endif()
endif()

include(CTest)

add_subdirectory(src)