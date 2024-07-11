cmake_minimum_required(VERSION 3.11.0)
project(pizzas)

set(CMAKE_CXX_STANDARD 17)
set(SRC_LIST src/Funghi.cpp src/Margherita.cpp src/Pizza.cpp src/Pizzeria.cpp)
set(TEST_SRC_LIST test/test_main.cpp)


include(FetchContent)
FetchContent_Declare (googletest GIT_REPOSITORY https://github.com/google/googletest.git GIT_TAG v1.14.0)
set (gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

include_directories(${CMAKE_SOURCE_DIR}/src)
find_package(Threads REQUIRED)

link_libraries(gmock)
add_library(${PROJECT_NAME}-lib STATIC ${SRC_LIST} ${TEST_SRC_LIST})
add_executable(${PROJECT_NAME} src/main.cpp ${CMAKE_THREAD_LIBS_INIT})
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)
target_link_libraries(${PROJECT_NAME}-lib Threads::Threads)

add_executable(${PROJECT_NAME}-ut test/PizzeriaTest.cpp)
target_link_libraries(${PROJECT_NAME}-ut ${PROJECT_NAME}-lib)

enable_testing()
add_test(NAME someTests COMMAND ${PROJECT_NAME}-ut)

