cmake_minimum_required(VERSION 3.11.0)

project(pizzas)

set(CMAKE_CXX_STANDARD 17)
set(SRC_LIST src/Funghi.cpp src/Margherita.cpp src/Pizza.cpp src/Pizzeria.cpp)

add_library(${PROJECT_NAME}-lib STATIC ${SRC_LIST})

add_executable(${PROJECT_NAME} src/main.cpp ${CMAKE_THREAD_LIBS_INIT})
find_package(Threads REQUIRED)

target_link_libraries(${PROJECT_NAME}-lib Threads::Threads)
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib )


