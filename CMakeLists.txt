# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.8)

project ("chlaus-cpp-template")

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release CACHE STRING "The configuration to build" FORCE)
endif()

set(CMAKE_CXX_FLAGS "-Wall -Wno-unsupported-friend -pedantic -std=c++17")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -fsanitize=address")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/out/${CMAKE_BUILD_TYPE}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/out/${CMAKE_BUILD_TYPE}/lib")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/out/${CMAKE_BUILD_TYPE}/lib")

option(BUILD_UNIT_TESTS "Build unit tests" ON)

include_directories("include" "/usr/local/include")

add_subdirectory(src)

# Include sub-projects.
#add_subdirectory ("chlaus-cpp-template")

if(${BUILD_UNIT_TESTS})
  enable_testing()
  add_subdirectory(tests)
endif()