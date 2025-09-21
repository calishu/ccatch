cmake_minimum_required(VERSION 4.0.0...4.0.3)
set(CMAKE_C_STANDARD 99)

project(ccatch VERSION 1.0 LANGUAGES C)

option(TESTS_ENABLED "Should the tests also be compiled?" OFF)

file(GLOB_RECURSE sources src/*.c)
file(GLOB_RECURSE tests tests/*.c tests/*.h)

add_library(ccatch_lib STATIC ${sources})
target_include_directories(ccatch_lib PUBLIC include)

if(TESTS_ENABLED)
  add_executable(ccatch_test ${tests})
  target_link_libraries(ccatch_test PRIVATE ccatch_lib)
  target_include_directories(ccatch_test PRIVATE include tests)
endif()
