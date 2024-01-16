cmake_minimum_required(VERSION 3.8.0)
project(jsoncpp VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include_directories(
        ${PROJECT_SOURCE_DIR}/include
        ${PROJECT_SOURCE_DIR}/lib)

# set runtime path
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/release/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/release/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/release/lib)

add_library(${PROJECT_NAME} STATIC
        ${PROJECT_SOURCE_DIR}/lib/json_reader.cpp
        ${PROJECT_SOURCE_DIR}/lib/json_value.cpp
        ${PROJECT_SOURCE_DIR}/lib/json_writer.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
    

add_subdirectory(example)