cmake_minimum_required(VERSION 3.5)

project(MODEL_LIB)

include(CheckIncludeFileCXX)

check_include_file_cxx(any HAS_ANY)
check_include_file_cxx(string_view HAS_STRING_VIEW)
check_include_file_cxx(ranges HAS_RANGES)

set(CMAKE_CXX_STANDARD 17)

if (MSVC)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
endif ()

set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_library(${PROJECT_NAME} STATIC)

find_package(Drogon CONFIG REQUIRED)

target_link_libraries(${PROJECT_NAME} PUBLIC Drogon::Drogon)

message(STATUS "Using C++17")

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/models MODEL_SRC)

target_include_directories(${PROJECT_NAME} PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>)

target_sources(${PROJECT_NAME} PUBLIC ${MODEL_SRC})
