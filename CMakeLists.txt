cmake_minimum_required(VERSION 3.11.0)

project(pizzas)

set(CMAKE_CXX_STANDARD 17)
set(SRC_LIST src/Funghi.cpp src/Margherita.cpp src/Pizza.cpp src/Pizzeria.cpp)
set(TEST_SRC_LIST test/PizzeriaTest.cpp test/test_main.cpp)

add_library(${PROJECT_NAME}-lib STATIC ${SRC_LIST})
add_executable(${PROJECT_NAME} src/main.cpp ${CMAKE_THREAD_LIBS_INIT})

find_package(Threads REQUIRED)
target_link_libraries(${PROJECT_NAME}-lib Threads::Threads)
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib )

include(FetchContent)
FetchContent_Declare (googletest URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip)

set (gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)
