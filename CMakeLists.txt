project(particle_filter)

cmake_minimum_required (VERSION 3.5)

add_definitions(-std=c++11)

set(CXX_FLAGS "-Wall")
set(CMAKE_CXX_FLAGS, "${CXX_FLAGS}")

FILE(GLOB SOURCES src/*.cpp)

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

include_directories(include)

include_directories(/usr/local/include)
include_directories(/usr/local/opt/openssl/include)
link_directories(/usr/local/lib)
link_directories(/usr/local/opt/openssl/lib)
link_directories(/usr/local/Cellar/libuv/1*/lib)

endif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

add_library(particle_filter ${SOURCES})
target_include_directories(particle_filter PUBLIC include)

add_executable(kidnapped_vehicle experiments/main.cpp)
target_link_libraries(kidnapped_vehicle particle_filter z ssl uv uWS)
