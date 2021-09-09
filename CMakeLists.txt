cmake_minimum_required(VERSION 3.19)

project(cppbackport VERSION ${PROJECT_VERSION} LANGUAGES CXX C)

if(EXISTS ${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    conan_basic_setup()
else()
    message(WARNING "The file conanbuildinfo.cmake doesn't exist, you have to run conan install first")
endif()

set(CMAKE_CXX_STANDARD 14)

file(GLOB SRC_FILES
    src/*.cpp
    src/fs/*.cpp
    src/traits/*.cpp
)

add_library(${PROJECT_NAME} ${SRC_FILES})

target_include_directories(${PROJECT_NAME}
    PRIVATE
    PUBLIC
        include
    INTERFACE
)

target_link_libraries(${PROJECT_NAME}
    PRIVATE
        ${CONAN_LIBS}
    PUBLIC
    INTERFACE
)

set_target_properties(${PROJECT_NAME}
    PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION 1
)
