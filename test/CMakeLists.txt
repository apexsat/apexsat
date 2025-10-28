# Testing only CMakeLists.txt
cmake_minimum_required(VERSION 3.22)
project(Testing)

set (CMAKE_CXX_STANDARD 17)
set (CMAKE_CXX_STANDARD_REQUIRED ON)

# --- Fetch GoogleTest ---
# This downloads and configures GTest automatically
include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)
# For Windows: Prevent overriding the parent project's compiler settings.
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

enable_testing()

add_executable(testing)
target_sources(testing
  PRIVATE
    test.cpp

    # Add source files here

    # Core/Src/main.c
)
target_link_libraries(
  testing
  GTest::gtest_main
)
# target_include_directories(testing PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/Core/Src)

include(GoogleTest)
gtest_discover_tests(testing)