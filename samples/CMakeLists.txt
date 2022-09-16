cmake_minimum_required(VERSION 3.6)

include(CTest)

project(gmockglobal VERSION 1.1.8 LANGUAGES CXX)

enable_testing()

# GoogleTest requires at least C++14
set(CMAKE_CXX_STANDARD 14)

set(GTEST_VERSION)

include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest
  GIT_TAG        release-${GTEST_VERSION}
)
FetchContent_MakeAvailable(googletest)

set(SRC_LIST main.cpp)
set(SRC_HEADER include/gmock-global/gmocl-global.h)

add_library(MY_LIB
  ${SRC_LIST}
)

target_link_libraries(MY_LIB
  
  ${PROJECT_NAME}::${PROJECT_NAME}
  GTest::gtest_main
  GTest::gmock_main
)

add_executable(
    sample
    ${SRC_LIST}
)

target_link_libraries(sample
    MY_LIB
)

add_test (NAME GMOCK-GLOBAL_Test COMMAND sample)

