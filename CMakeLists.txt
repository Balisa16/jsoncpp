set(JSONCPP_OLDEST_VALIDATED_POLICIES_VERSION "3.8.0")
set(JSONCPP_NEWEST_VALIDATED_POLICIES_VERSION "3.13.2")
cmake_minimum_required(VERSION ${JSONCPP_OLDEST_VALIDATED_POLICIES_VERSION})

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Ensure that CMAKE_BUILD_TYPE has a value specified for single configuration generators.
if(NOT DEFINED CMAKE_BUILD_TYPE AND NOT DEFINED CMAKE_CONFIGURATION_TYPES)
    set(CMAKE_BUILD_TYPE Release CACHE STRING
        "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel Coverage.")
endif()

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

# ---------------------------------------------------------------------------
# use ccache if found, has to be done before project()
# ---------------------------------------------------------------------------

project(jsoncpp
        LANGUAGES CXX)

set(PROJECT_SOVERSION 25)

include_directories(${PROJECT_SOURCE_DIR}/include)

add_library(${PROJECT_NAME} SHARED
    lib/json_value.cc
    lib/json_reader.cc
    lib/json_writer.cc)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/release)

add_executable(test_strunner src/jsontestrunner/main.cpp)
target_link_libraries(test_strunner PRIVATE ${PROJECT_NAME})


set(INSTALL_LIB_DIR lib CACHE PATH "/usr/local/lib")
set(INSTALL_INCLUDE_DIR include CACHE PATH "/usr/local/include")

# Install the library
install(TARGETS ${PROJECT_NAME}
        EXPORT JSONCPPTargets
        ARCHIVE DESTINATION ${INSTALL_LIB_DIR}
)

file(GLOB HEADER_FILES ${PROJECT_SOURCE_DIR}/include/*.hpp)
# Install the header files
install(FILES ${HEADER_FILES}
        DESTINATION ${INSTALL_INCLUDE_DIR}/jsoncpp
)