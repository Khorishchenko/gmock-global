cmake_minimum_required(VERSION 3.0)

project(plog VERSION 1.1.8 LANGUAGES CXX)

# GoogleTest requires at least C++14
set(CMAKE_CXX_STANDARD 14)

set(GTEST_VERSION)

include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG        release-${GTEST_VERSION}
)
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

set(SRC_LIST main.cpp)

add_library(MY_LIB
  ${SRC_LIST}
)

target_link_libraries(MY_LIB
  
  ${PROJECT_NAME}::${PROJECT_NAME}
  GTest::gtest_main
  GTest::gmock_main
)